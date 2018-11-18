# My_Meal-
# A web application that allows employees to order lunch from predefined menu

from flask import *
import os
import sqlite3
app = Flask(__name__, static_url_path='')

a=open("a.html","r")

a=a.read()
d=open(os.getcwd()+"/prot/users.html","r")
admin="123"
op=open(os.getcwd()+"/a.html","r")
d=d.read()
im=open("My lunch.html","r")
im=im.read()

ah=im
print(ah)
conn=sqlite3.connect("pass.db")
c=conn.cursor()
try:
	c.execute("""CREATE TABLE pas(
         name text,
          pass text
          )""")
except:
	
	b=1


@app.route('/')
def hello_world():
   return a
@app.route('/login',methods=["GET","POST"])
def login():
   if request.method=="POST":
      if request.form["name"]=="admin":
         if request.form["password"]==admin:
            return d
      else:
              
              
              
                conn=sqlite3.connect("pass.db")
                c=conn.cursor()
                c.execute("SELECT * FROM pas WHERE name='"+str(request.form["name"]+"'"))
                abc=c.fetchall()
                print(abc[0][1])
                if abc[0][1]==request.form["password"]:
                        
                        
                        conn.commit()

                        conn.close()
                        ah=im
                       
                        
                        
                        return ah
                else:
                        return "<h1>worng passowrd</h1>"
@app.route('/add_user',methods=["GET","POST"])
def add_user():
   if request.method=="POST":
                conn=sqlite3.connect("pass.db")
                c=conn.cursor()
                u=str(request.form["name"])
                b=str(request.form["password"])
                c.execute("INSERT INTO pas VALUES('"+u+"','"+b+"')")
                conn.commit()

                conn.close()
                return d

@app.route("/rm_user",methods=["POST","GET"])
def rm_user():
        conn=sqlite3.connect("pass.db")
        c=conn.cursor()
        c.execute("SELECT * FROM pas WHERE name='"+request.form["name"]+"'")
        if c.fetchall:
                        
                c.execute("DELETE from pas WHERE name='"+request.form["name"]+"'")
                           
                            
                conn.commit()
                conn.close()
        return d
        
@app.route('/view',methods=["GET","POST"])
def view():
        
                
        conn=sqlite3.connect("pass.db")
        c=conn.cursor()
        j='<div><lu><style>div{color:blue}</style>'
        c.execute("SELECT * FROM pas ")
        if c.fetchall:
                        
                         
                         
                if request.method=='POST':
                        
                        for i in c.fetchall():

                                j+="<li>"+i[0]+" "+i[1]+"</li>"
                                
                                    
                                lis=c.fetchall()
                                i=0
                        
                                    
                                    
                                    
                                        
                                        #j+='<li>'+lis[i-1][0]+" "+lis[i-1][1]+"</li>"
                        j+="</lu></div>"
                        return j

@app.route('/order',methods=["GET","POST"])
def order():
        print("hi")
        
        return "<h1>you orderd item number:</h1>"+request.form["fname"]
@app.route('/remov_item',methods=["GET","POST"])
def remov():
        a=im
        a=a.replace("<h3>"+request.form['name']," ")
        return d
        
                  
if __name__ == '__main__':
        
        app.run()
