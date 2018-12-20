[TOC]

## demo
api
```
func HealthCheckHandler(w http.ResponseWriter, r *http.Request) {
	r.Header.Add("Content-Type", "application/x-www-form-urlencoded")

	name := r.FormValue("name")
	age := r.FormValue("age")
	json :=fmt.Sprintf(`{"name":"%s","age":"%s"}`,name,age)

	io.WriteString(w, json)
}

func main(){
	http.HandleFunc("/health-check",HealthCheckHandler)
	e := http.ListenAndServe(":7010", nil)
	if e != nil {
		log.Println(e)
	}
}
```
apitest
```
func TestApi(t *testing.T) {
	data := url.Values{}
	data.Add("name","cpj")
	data.Add("age","1")
	r := httptest.NewRequest(http.MethodPost, "/health-check", strings.NewReader(data.Encode()),
	)
	//在测试时,或 api 接口 必须声明 是 x-www-form-urlencoded
	r.Header.Add("Content-Type", "application/x-www-form-urlencoded")
	r.Header.Set("commpay", "brk")

	w := httptest.NewRecorder()
	HealthCheckHandler(w, r)

	result := w.Result()

	body, _ := ioutil.ReadAll(result.Body)

	//是否是200
	if result.StatusCode != http.StatusOK {
		t.Errorf("expected status 200,",result.StatusCode)
	}

	resjson :=`{"name":"cpj","age":"1"}`
	if resjson != string(body) {
		t.Error("返回结果不正确",string(body))
	}

}
```