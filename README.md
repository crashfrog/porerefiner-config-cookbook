# porerefiner-config-cookbook
Notifier/Job/Submitter examples for PoreRefiner

Config Files
------------

Here's my entire config.yaml:

    database:
      path: /Users/justin.payne/.porerefiner/database.db
      pragmas:
      cache_size: 1000
      foreign_keys: 1
      ignore_check_constraints: 0
      journal_mode: wal
      synchronous: 0
    nanopore:
      api: localhost:9501
      path: /data
    porerefiner:
      job_polling_interval: 1800
      log_level: 20
      run_polling_interval: 600
    server:
      socket: /Users/justin.payne/.porerefiner/socket
      use_ssl: false
    submitters:
    - class: HpcSubmitter
      config:
        login_host: login1-raven2.fda.gov
        username: nanopore
        private_key_path: /root/.ssh/nanopore
        known_hosts_path: /root/.ssh/known_hosts
        scheduler: uge
        queue: service.q
      jobs:
      - class: FdaRunJob
        config:
        command: module load nanopore-lims/0.1.0 && nanopore_HPC {remote_json} &
        platform: GridION sequence
        closure_status_recipients:
        - justin.payne@fda.hhs.gov
        import_ready_recipients:
        - justin.payne@fda.hhs.gov
      
From here on in we'll just provide the last stanza, `submitters`, for instance:

    submitters:
    - class: HpcSubmitter
      config:
        login_host: login1-raven2.fda.gov
        username: nanopore
        private_key_path: /root/.ssh/nanopore
        known_hosts_path: /root/.ssh/known_hosts
        scheduler: uge
        queue: service.q
      jobs:
      - class: FdaRunJob
        config:
          command: module load nanopore-lims/0.1.0 && nanopore_HPC {remote_json} &
          platform: GridION sequence
          closure_status_recipients:
          - justin.payne@fda.hhs.gov
          import_ready_recipients:
          - justin.payne@fda.hhs.gov
