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
