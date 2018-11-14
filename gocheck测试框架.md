[TOC]

## 常用断言快速入门
```
package hello_test
import (
	"github.com/pkg/errors"
	"testing"
	. "gopkg.in/check.v1"
)
func Test(t *testing.T) { TestingT(t) }
type MySuite struct{}
var _ = Suite(&MySuite{})
func (s *MySuite) TestHelloWorld(c *C) {
	value := 42
	array :=[]string{"hi","there"}
	err := errors.New("perm.*denied")
	list := []string{"name","asda"}
	var err1 error

	c.Assert(value, DeepEquals, 42)
	c.Assert(array, DeepEquals, []string{"hi", "there"})
	c.Assert(value, Not(Equals), 43)
	c.Assert(value, Equals, 42)
	c.Assert(err, ErrorMatches, "perm.*denied")
	c.Assert(list, HasLen, 2)
	c.Assert(err1, IsNil)
}
```
## 文件操作相关的单元测试
```
package main

import (
	"testing"
	"io/ioutil"

	. "gopkg.in/check.v1"
)

const txt = "adfagaggafaf"

func Test(t *testing.T) { TestingT(t) }

type MySuite struct {
	dir string   // 测试用的临时目录
	f   string   // 测试用的临时文件
}

var _ = Suite(&MySuite{})

// Setupsuite 准备测试用的临时文件
func (s *MySuite) SetUpSuite(c *C) {
	dir := c.MkDir()    // Suite结束后会自动销毁c.MkDir()创建的目录

	tmpfile, err := ioutil.TempFile(dir, "")
	if err != nil {
		c.Errorf("Fail to create test file: %v\n", tmpfile.Name(), err)
	}

	err = ioutil.WriteFile(tmpfile.Name(), []byte(txt),0777) //tmpfile.Name() C:\Users\idcpj\AppData\Local\Temp\check-6334824724549167320\0\143714611
	if err != nil {
		c.Errorf("Fail to prepare test file.%v\n", tmpfile.Name(), err)
	}
	//把创建的文件和目录保存到 MySuite下
	s.dir = dir
	s.f = tmpfile.Name()
}

func (s *MySuite) TestFoo(c *C) {
	// ... 实际测试代码
	c.Assert(bkpName, Matches, s.f+".ops_agent_bkp.+")
}
```
## 

## 创建一个用例组
```
var _ = check.Suite(&MySuite{})
```

## 预热或者清理回收
```
func (s *SuiteType) SetUpSuite(c *C) //用例组数据或对象准备
func (s *SuiteType) SetUpTest(c *C)  //单用例数据或对象准备
func (s *SuiteType) TearDownTest(c *C) //单用例后续数据回收及对象清理
func (s *SuiteType) TearDownSuite(c *C) //用例组数据回收及对象清理
```

