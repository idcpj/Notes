[TOC]

## 快速入门
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

