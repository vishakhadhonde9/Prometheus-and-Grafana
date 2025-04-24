# Prometheus -
- Prometheus is monitoring tool.
- Prometheus is an open-source monitoring and alerting toolkit, originally developed by SoundCloud.
- Prometheus is a tool that watches your systems and applications and keeps track of how they are doing like how much CPU they’re using, how fast they respond, how many requests they’re handling, etc.
- It’s designed for recording real-time metrics in a time-series database with powerful queries and visualizations.

# Prometheus Configuration -


        sudo tee /etc/yum.repos.d/prometheus.repo <<EOF
        [prometheus]
        name=Prometheus
        baseurl=https://packagecloud.io/prometheus-rpm/release/el/7/x86_64
        repo_gpgcheck=1
        enabled=1
        gpgkey=https://packagecloud.io/prometheus-rpm/release/gpgkey https://raw.githubusercontent.com/lest/prometheus-rpm/master/RPM-GPG-KEY-prometheus-rpm
        gpgcheck=1
        metadata_expire=300
        EOF

      - sudo yum update -y
      - sudo yum -y install prometheus2 node_exporter
      - rpm -qi prometheus2
      - sudo systemctl start prometheus node_exporter
      - systemctl status prometheus.service node_exporter.service
      - add port 9090 in security group
      - copy ec2 public IP and paste in browser with port no 9090
      - now you should see prometheus dashboard
      
      
# /etc/prometheus/prometheus.yml -

                rule_files:
                    - "rules.yml"
                  # - "second_rules.yml"
                
                # A scrape configuration containing exactly one endpoint to scrape:
                # Here it's Prometheus itself.
                scrape_configs:
                  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
                  - job_name: "prometheus"
                
                    # metrics_path defaults to '/metrics'
                    # scheme defaults to 'http'.
                
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
                
