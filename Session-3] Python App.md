# Python Application - /etc/prometheus/app.py

          import http.server
          from prometheus_client import start_http_server
          from prometheus_client import Counter,generate_latest, CONTENT_TYPE_LATEST
          from flask import Flask
          
          app = Flask(__name__)
          REQUESTS = Counter('hello_worlds_total','Hello Worlds requested.')
          @app.route('/')
          def hello_world():
              REQUESTS.inc()
              return 'Hello, World!'
          
          @app.route('/metrics')
          def metrics():
              return generate_latest(), 200, {'Content-Type': CONTENT_TYPE_LATEST}
          
          
          if __name__ == '__main__':
              # Run the Flask app and listen on all network interfaces
               #start_http_server(8000)
               app.run(host='0.0.0.0', debug=True)


## Configuartion file -

      static_configs:
            - targets: ["localhost:9090"]
        - job_name: "node"
      
          # metrics_path defaults to '/metrics'
          # scheme defaults to 'http'.
      
          static_configs:
            - targets: ["localhost:9100"]
        - job_name: "app"
      
          # metrics_path defaults to '/metrics'
          # scheme defaults to 'http'.
      
          static_configs:
            - targets: ["localhost:5000"]
      
  - Add port 5000 to sg.
        
  ## Installation for application -    
      
   sudo yum install python3-pip
   pip3 install prometheus_client
   pip install flask
   python3 app.py --> to run file










               
