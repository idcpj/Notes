[TOC]

## 实例
```
class  AysMysql{
    public  $dbSource="";
    private $dbconfig;

    public function __construct(){
        $this->dbSource = new swoole_mysql();
        $this->dbconfig=[
            'host'=>'127.0.0.1',
            'port'=>3306,
            'user'=>'root',
            'password'=>'12345678',
            'database'=>'demo',
            'charset'=>'utf8',
        ];
    }

    public function update(){

    }

    public function add(){

    }

    public function execute($id, $username){
        $this->dbSource->connect($this->dbconfig,function($db,$result) use ($username, $id){
            echo  "connect...".PHP_EOL;
            //错误
            if($result === false){
                var_dump($db->connect_error);
            }
            //$sql = "select * from test where id=1 LIMIT 1";
            $sql = "update test set username='{$username}' WHERE id='{$id}'";

            //增删改查 都可以用 query
            $db->query($sql,function($db,$result){
                if ($result===false){
                    //todo
                    print_r($db->error);
                }elseif($result===true){
                    //todo
                    print_r($db->affected_rows);
                }else{
                    print_r($result);
                }
                $db->close();

            });


        });
        return true;
    }
}

$obj = new AysMysql();
$obj->execute(1,'idcpj2');

echo  "start".PHP_EOL;


```