# library-management

import mysql.connector as a

con = a.connect(host='localhost', 
                user='balub', 
                passwd='uma9392@', 
                database='library',
                auth_plugin='mysql_native_password')

def addbook():
    bn=input("Enter Book name:")
    c=input("Enter book code:")
    t=input("total books:")
    s=input("enter subject:")
    data=(bn,c,t,s)
    sql='insert into books values(%s,%s,%s,%s)'
    c=con.cursor()
    c.execute(sql,data)
    con.commit()
    print(">------------------------------------")
    print('data enterd succesfully')
    main()
    
def issueb():
    n=input('enter name:')
    r=input('enter reg no:')
    co=input('enter book code:')
    d=input('enter date:')
    a="insert into issue values(%s,%s,%s,%s)"
    data=(n,r,co,d)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    print(">................................")
    print("book issued to:",n)
    bookup(co,-1)
    
def submitb():
    n=input('enter name:')
    r=input('enter reg no:')
    co=input('enter book code:')
    d=input('enter date:')
    a="insert into submit values(%s,%s,%s,%s)"
    data=(n,r,co,d)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    print(">................................")
    print("book submitted from:",n)
    bookup(co,1)
    
def bookup(co,u):
    a="select total from books where BCODE=%s"
    data=(co,)
    c=con.cursor()
    c.execute(a,data)
    myresult=c.fetchone()
    t=myresult[0]+u
    sql="update books set TOTAL =%s where BCODE=%s"
    d=(t,co)
    c.execute(sql,d)
    con.commit()
    main()

def dbook():
    ac=input("enter book code:")
    a="delete from books where BCODE=%s"
    data=(ac,)
    c=con.cursor()
    c.execute(a,data)
    con.commit()
    main()

def dispbook():
    a="select * from books"
    c=con.cursor()
    c.execute(a)
    myresult=c.fetchall()
    for i in myresult:
        print("book Name :",i[0])
        print("book code:",i[1])
        print("total:",i[2])
        print("subject:",i[3])
        print(">....................<")
    main()
        
def main():
    print("""
    1.ADD BOOK
    2.ISSUE BOOK
    3.SUBMIT BOOK
    4.DELETE BOOK
    5.DISPLAY BOOK""")
    choice=input("enter task no:")
    print(">-------------------------------------------------------------<")
    if(choice=='1'):
        addbook()
    elif(choice=='2'):
        issueb()
    elif(choice=='3'):
        submitb()
    elif(choice=='4'):
        dbook()
    elif(choice=='5'):
        dispbook()
    else:
        print("wrong choice.....")
def pswd():
    ps=input('enter password:')
    if ps=="uma9392@":
        main()
    else:
        print('wrong pass')
        pswd()
pswd()
