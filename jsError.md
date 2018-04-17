```js
    <script>
      // 简单的将错误采集上报到 /api/logs/error
      window.onerror = function(message, source, lineno, colno, error) {
        try {
          var msg = {
            message: message,
            source: source,
            lineno: lineno,
            colno: colno,
            stack: error.stack,
            traceId: window.appData && window.appData.traceId,
            href: window.location.href,
          };
          msg = JSON.stringify(msg);
          var req = new XMLHttpRequest();
          req.open('post', '/api/logs/error', true);
          req.setRequestHeader('Content-Type', 'application/json');
          req.send(msg);
        } catch (err) {
          console.log('report error', err);
        }
      };
    </script>
```
