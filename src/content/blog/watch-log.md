---
title: WatchLogs
description: ""
pubDate: "2024-07-08"
---

```go
package main

import (
	"log"
	"strings"
	"time"

	"github.com/fsnotify/fsnotify"
)

func main() {
	watcher, err := fsnotify.NewWatcher()
	if err != nil {
		log.Fatal(err)
	}
	defer watcher.Close()

	done := make(chan bool)

	go func() {
		for {
			select {
			case event, ok := <-watcher.Events:
				if !ok {
					return
				}
				if event.Op&fsnotify.Write == fsnotify.Write {
					// 读取文件内容并匹配字符串
					content, err := readFileContent(event.Name)
					if err != nil {
						log.Println("读取文件内容错误:", err)
						continue
					}
					if strings.Contains(content, "abcde") {
						log.Println("匹配到字符串 'abcde'")
					}
				}
			case err, ok := <-watcher.Errors:
				if !ok {
					return
				}
				log.Println("错误:", err)
			}
		}
	}()

	// 替换为你要监听的日志文件路径
	watchPath := "/path/to/your/logfile.log"
	err = watcher.Add(watchPath)
	if err != nil {
		log.Fatal(err)
	}

	<-done
}

func readFileContent(filename string) (string, error) {
	// 这里假设每次写入都是追加操作，只读取文件末尾的新内容
	// 实际实现可能需要根据具体情况调整
	data, err := os.ReadFile(filename)
	if err != nil {
		return "", err
	}
	return string(data), nil
}
```
