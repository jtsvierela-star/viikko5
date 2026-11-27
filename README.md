Another try for readme file.
ubuntu@tuomas1linux:~$ ollama list
NAME            ID              SIZE      MODIFIED     
qwen2.5:0.5b    a8b0c5157701    397 MB    22 hours ago  

ubuntu@tuomas1linux:~$ ss -ltnp
State       Recv-Q      Send-Q           Local Address:Port             Peer Address:Port      Process                                                                                              
LISTEN      0           511                    0.0.0.0:80                    0.0.0.0:*                                                                                                              
LISTEN      0           4096                   0.0.0.0:22                    0.0.0.0:*                                                                                                              
LISTEN      0           2048                 127.0.0.1:5000                  0.0.0.0:*          users:(("gunicorn",pid=405846,fd=3),("gunicorn",pid=405837,fd=3),("gunicorn",pid=405826,fd=3))      
LISTEN      0           4096                 127.0.0.1:11434                 0.0.0.0:*                                                                                                              
LISTEN      0           4096                127.0.0.54:53                    0.0.0.0:*                                                                                                              
LISTEN      0           80               192.168.1.182:3306                  0.0.0.0:*                                                                                                              
LISTEN      0           4096             127.0.0.53%lo:53                    0.0.0.0:*                                                                                                              
LISTEN      0           511                       [::]:80                       [::]:*                                                                                                              
LISTEN      0           4096                      [::]:22                       [::]:*                                                                                                              
ubuntu@tuomas1linux:~$ 

## Request Path – Application Architecture

The communication between the user, the application, the language model, and the database follows this request path:

```text
┌──────────────────────┐
│ Browser              │
│ Chat interface       │
└──────────┬───────────┘
           │ HTTP
           ▼
┌──────────────────────┐
│ Nginx                │
│ Port 80              │
└──────────┬───────────┘
           │ Unix socket
           ▼
┌──────────────────────┐
│ Gunicorn             │
│ Flask application   │
│ /run/chatapp/        │
│ gunicorn.sock        │
└──────────┬───────────┘
           │
           ├──────────────────────┐
           │                      │
           ▼                      ▼
┌──────────────────────┐  ┌──────────────────────┐
│ Ollama               │  │ MariaDB              │
│ Qwen2.5:0.5b         │  │ Chat history         │
│ 127.0.0.1:11434      │  │ chatapp database    │
└──────────────────────┘  └──────────────────────┘
```

### Request Flow

1. The user enters a message in the chat interface in the browser.
2. The browser sends an HTTP request to Nginx at `/viikko5/`.
3. Nginx forwards the request to Gunicorn through the Unix socket `/run/chatapp/gunicorn.sock`.
4. Gunicorn runs the Flask application, which processes the user's message.
5. Flask sends the prompt to the local Ollama model server at `127.0.0.1:11434`.
6. Ollama uses the Qwen2.5:0.5b language model to generate a response.
7. Flask stores the conversation in the MariaDB database and returns the response to the browser through Nginx.
a description of the pipeline: what runs on pull requests, what runs on main, and how a deployment is verified:
the Linux users, database users, file ownership and permissions you used, and where the secrets are stored
how you added /viikko5/ to Nginx without affecting other sites or pages
your model choice and the server's memory and disk usage
if you completed Week 4: whether the chat database is replicated to server B, and why or why not
the required test results
one problem you solved or one thing you learned