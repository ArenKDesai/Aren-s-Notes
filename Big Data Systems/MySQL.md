#CS544 #UWMadison #MySQL #SQL 

### Basic Commands
```{Python}
from sqlalchemy import create_engine, text
engine = create_engine("mysql+mysqlconnector://root:abc127.0..0.1:3306/cs544")
conn.connect()

conn.execute(text("update accounts set amount=amount-1 where name='a'"))

conn.commit()
# or conn.rollback()
```
show tables; -> shows all tables in mysql databse