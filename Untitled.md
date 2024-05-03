## 日志配置
```yaml
logs:
    
    - name: your name 1

      level: debug/info/error/fatal/DEUBG/...
    
      appenders:
    
          - type: FileLogAppender
    
            file: /home/hhhyh/logs/sylar/root.txt
    
    
    - name: your name 2
    
      level: ...
    
      appenders:
    
          - type: StdoutLogAppender
    
    ...
```