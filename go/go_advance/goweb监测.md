import _ "net/http/pprof"

func main(){
  go func(){
  log.Error(http.ListenAndServe(":6060",nil))
}
}

加入代码中
http://localhost:6060/debug/pprof