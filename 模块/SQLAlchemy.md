[TOC]


## SQLAlchemy 
`pip install SQLAlchemy`
>window 需要安装 `pip install mysqlclient`

### 连接
```
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

engine = create_engine('mysql+mysqldb://root:root@localhost:3306/blog')

Base = declarative_base()


class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    username = Column(String(64), nullable=False, index=True)
    password = Column(String(64), nullable=False)
    email = Column(String(64), nullable=False, index=True)

    def __repr__(self):
        return '%s(%r)' % (self.__class__.__name__, self.username)


Base.metadata.create_all(engine)
```
1. 一对多关系
方法一
```python
class User(Base):
    articles = relationship('Article')

class Article(Base):
	 user_id = Column(Integer, ForeignKey('users.id')) #多的一方用外键
     author = relationship('User')
```
方法二

```python
class User(Base):
	__tablename__='users'
    articles = relationship('Article', backref='user')
class Article(Base):
	__tablename__='articles'
	 user_id = Column(Integer, ForeignKey('users.id'))
```
*对relationship('Article', backref='user')注解*

`Article`表示对应`Article`类,`user`作用是在插入数据时,`user_id`用`user`代替如下
```python
article = Article(
    title=faker.sentence(),
    content=' '.join(faker.sentences(nb=random.randint(10, 20))),
    user=random.choice(faker_users),  #此处的user既是backref的值
    category=random.choice(faker_categories)
)
```
2. 一对一
```
class User(Base):
    userinfo = relationship('UserInfo', backref='user', uselist=False)
    
class Article(Base):
	 user_id = Column(Integer, ForeignKey('users.id'))
```
### 操作数据
```
Session = sessionmaker(bind=engine)
session = Session()

    # 查询
    UserOne = session.query(User).get(1)
    print(UserOne.username);

    # 条件查询
    UserOne = session.query(User).filter_by(username='Scott Black').first()
    print(UserOne.username);
    # 查询多个
    UserOne = session.query(User).filter_by(username='Scott Black').all()
    print(UserOne);

    # 更新
    a = session.query(Article).get(10)
    a.title = 'My test blog post'
    session.add(a)
    session.commit()

    # 删除
    a = session.query(Article).get(10)
    session.delete(a)
    session.commit()

```