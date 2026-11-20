---
dataset_info:
- config_name: env_bank_database
  features:
  - name: suite
    dtype: string
  - name: account_list
    list:
    - name: balance
      dtype: float64
    - name: iban
      dtype: string
    - name: transactions
      list:
      - name: id
        dtype: int64
      - name: sender
        dtype: string
      - name: recipient
        dtype: string
      - name: amount
        dtype: float64
      - name: subject
        dtype: string
      - name: date
        dtype: string
      - name: recurring
        dtype: bool
    - name: scheduled_transactions
      list:
      - name: id
        dtype: int64
      - name: sender
        dtype: string
      - name: recipient
        dtype: string
      - name: amount
        dtype: float64
      - name: subject
        dtype: string
      - name: date
        dtype: string
      - name: recurring
        dtype: bool
    - name: password
      dtype: string
    - name: verification
      dtype: bool
  - name: current_account
    dtype: string
  splits:
  - name: train
    num_bytes: 2718
    num_examples: 3
  download_size: 12838
  dataset_size: 2718
- config_name: env_calendar
  features:
  - name: suite
    dtype: string
  - name: current_day
    dtype: string
  - name: account_email
    dtype: string
  - name: initial_events
    list:
    - name: id_
      dtype: string
    - name: title
      dtype: string
    - name: description
      dtype: string
    - name: start_time
      dtype: string
    - name: end_time
      dtype: string
    - name: location
      dtype: string
    - name: participants
      list: string
    - name: all_day
      dtype: bool
    - name: status
      dtype: string
  - name: events
    list:
    - name: _key
      dtype: string
    - name: id_
      dtype: string
    - name: title
      dtype: string
    - name: description
      dtype: string
    - name: start_time
      dtype: string
    - name: end_time
      dtype: string
    - name: location
      dtype: string
    - name: participants
      list: string
    - name: all_day
      dtype: bool
    - name: status
      dtype: string
  splits:
  - name: train
    num_bytes: 4825
    num_examples: 3
  download_size: 15657
  dataset_size: 4825
- config_name: env_email_database
  features:
  - name: suite
    dtype: string
  - name: inbox_list
    list:
    - name: account_email
      dtype: string
    - name: initial_emails
      list:
      - name: id_
        dtype: string
      - name: sender
        dtype: string
      - name: recipients
        list: string
      - name: cc
        list: 'null'
      - name: bcc
        list: 'null'
      - name: subject
        dtype: string
      - name: body
        dtype: string
      - name: status
        dtype: string
      - name: read
        dtype: bool
      - name: timestamp
        dtype: string
      - name: attachments
        list: string
    - name: emails
      list:
      - name: _key
        dtype: string
      - name: id_
        dtype: string
      - name: sender
        dtype: string
      - name: recipients
        list: string
      - name: cc
        list: 'null'
      - name: bcc
        list: 'null'
      - name: subject
        dtype: string
      - name: body
        dtype: string
      - name: status
        dtype: string
      - name: read
        dtype: bool
      - name: timestamp
        dtype: string
      - name: attachments
        list: string
    - name: contact_list
      list:
      - name: email
        dtype: string
      - name: name
        dtype: string
    - name: trash
      list: 'null'
    - name: received
      list:
      - name: id_
        dtype: string
      - name: sender
        dtype: string
      - name: recipients
        list: string
      - name: cc
        list: 'null'
      - name: bcc
        list: 'null'
      - name: subject
        dtype: string
      - name: body
        dtype: string
      - name: status
        dtype: string
      - name: read
        dtype: bool
      - name: timestamp
        dtype: string
      - name: attachments
        list: string
    - name: sent
      list:
      - name: id_
        dtype: string
      - name: sender
        dtype: string
      - name: recipients
        list: string
      - name: cc
        list: 'null'
      - name: bcc
        list: 'null'
      - name: subject
        dtype: string
      - name: body
        dtype: string
      - name: status
        dtype: string
      - name: read
        dtype: bool
      - name: timestamp
        dtype: string
      - name: attachments
        list: string
    - name: drafts
      list: 'null'
  - name: current_account
    dtype: string
  splits:
  - name: train
    num_bytes: 42968
    num_examples: 3
  download_size: 72955
  dataset_size: 42968
- config_name: env_filesystem
  features:
  - name: suite
    dtype: string
  - name: content
    dtype: string
  splits:
  - name: train
    num_bytes: 18643
    num_examples: 3
  download_size: 4866
  dataset_size: 18643
- config_name: env_github_platform
  features:
  - name: suite
    dtype: string
  - name: content
    dtype: string
  splits:
  - name: train
    num_bytes: 18962
    num_examples: 2
  download_size: 4045
  dataset_size: 18962
- config_name: env_shopping_platform
  features:
  - name: suite
    dtype: string
  - name: account_list
    list:
    - name: user_info
      struct:
      - name: first_name
        dtype: string
      - name: last_name
        dtype: string
      - name: ID_number
        dtype: string
      - name: email
        dtype: string
      - name: phone_number
        dtype: string
      - name: address
        dtype: string
      - name: passport_number
        dtype: string
      - name: bank_account_number
        dtype: string
      - name: bank_account_password
        dtype: string
    - name: username
      dtype: string
    - name: password
      dtype: string
    - name: verification
      dtype: bool
    - name: order_history
      list:
      - name: product_id
        dtype: string
      - name: product_name
        dtype: string
      - name: description
        dtype: string
      - name: price
        dtype: float64
      - name: brand
        dtype: string
      - name: category
        dtype: string
      - name: discount
        dtype: string
      - name: quantity
        dtype: int64
      - name: order_id
        dtype: string
      - name: payment
        dtype: float64
      - name: order_date
        dtype: string
      - name: delivery_date
        dtype: string
    - name: cart
      list:
      - name: product_id
        dtype: string
      - name: product_name
        dtype: string
      - name: description
        dtype: string
      - name: price
        dtype: float64
      - name: brand
        dtype: string
      - name: category
        dtype: string
      - name: discount
        dtype: 'null'
      - name: quantity
        dtype: int64
    - name: discount_list
      list:
      - name: code
        dtype: string
      - name: percentage
        dtype: float64
  - name: product_list
    list:
    - name: product_id
      dtype: string
    - name: product_name
      dtype: string
    - name: description
      dtype: string
    - name: price
      dtype: float64
    - name: brand
      dtype: string
    - name: category
      dtype: string
    - name: rating
      dtype: float64
    - name: reviews
      list: string
  - name: current_account_username
    dtype: string
  splits:
  - name: train
    num_bytes: 41183
    num_examples: 2
  download_size: 64218
  dataset_size: 41183
- config_name: env_web_database
  features:
  - name: suite
    dtype: string
  - name: web_list
    list:
    - name: web_url
      dtype: string
    - name: web_content
      dtype: string
    - name: field_to_parameters
      struct:
      - name: email_field
        dtype: string
      - name: account_id
        dtype: string
      - name: password_field
        dtype: string
      - name: comment_field
        dtype: string
      - name: username_field
        dtype: string
      - name: size_field
        dtype: string
      - name: time_field
        dtype: string
    - name: web_function
      list:
      - name: handler
        dtype: string
      - name: static_parameters
        struct:
        - name: body
          dtype: string
        - name: sender
          dtype: string
        - name: subject
          dtype: string
        - name: attachments
          list:
          - name: file_id
            dtype: string
          - name: type
            dtype: string
        - name: code
          dtype: string
        - name: percentage
          dtype: float64
        - name: amount
          dtype: int64
        - name: date
          dtype: string
        - name: recipient
          dtype: string
        - name: new_password
          dtype: string
        - name: file_id
          dtype: string
        - name: save_dir
          dtype: string
        - name: collaborator_email
          dtype: string
        - name: repo_name
          dtype: string
        - name: password_groundtruth
          dtype: string
        - name: recipients
          dtype: string
        - name: username_groundtruth
          dtype: string
        - name: return_str
          dtype: string
        - name: reservation
          dtype: string
    - name: web_requests
      list: 'null'
    - name: download_source
      dtype: string
  - name: file_list
    list:
    - name: _key
      dtype: string
    - name: type
      dtype: string
    - name: content
      dtype: string
    - name: permissions
      list:
      - name: _key
        dtype: string
      - name: value
        dtype: bool
    - name: source_name
      dtype: string
  splits:
  - name: train
    num_bytes: 44828
    num_examples: 3
  download_size: 63876
  dataset_size: 44828
- config_name: injection_tasks
  features:
  - name: suite
    dtype: string
  - name: GOAL
    dtype: string
  splits:
  - name: train
    num_bytes: 3078
    num_examples: 28
  download_size: 3428
  dataset_size: 3078
- config_name: tools
  features:
  - name: suite
    dtype: string
  - name: tool_name
    dtype: string
  - name: name
    dtype: string
  - name: description
    dtype: string
  - name: dependencies
    dtype: string
  - name: full_docstring
    dtype: string
  - name: return_type
    dtype: string
  splits:
  - name: train
    num_bytes: 52220
    num_examples: 100
  download_size: 17923
  dataset_size: 52220
- config_name: user_tasks
  features:
  - name: suite
    dtype: string
  - name: PROMPT
    dtype: string
  splits:
  - name: train
    num_bytes: 10175
    num_examples: 60
  download_size: 6382
  dataset_size: 10175
configs:
- config_name: env_bank_database
  data_files:
  - split: train
    path: env_bank_database/train-*
- config_name: env_calendar
  data_files:
  - split: train
    path: env_calendar/train-*
- config_name: env_email_database
  data_files:
  - split: train
    path: env_email_database/train-*
- config_name: env_filesystem
  data_files:
  - split: train
    path: env_filesystem/train-*
- config_name: env_github_platform
  data_files:
  - split: train
    path: env_github_platform/train-*
- config_name: env_shopping_platform
  data_files:
  - split: train
    path: env_shopping_platform/train-*
- config_name: env_web_database
  data_files:
  - split: train
    path: env_web_database/train-*
- config_name: injection_tasks
  data_files:
  - split: train
    path: injection_tasks/train-*
- config_name: tools
  data_files:
  - split: train
    path: tools/train-*
- config_name: user_tasks
  data_files:
  - split: train
    path: user_tasks/train-*
---
