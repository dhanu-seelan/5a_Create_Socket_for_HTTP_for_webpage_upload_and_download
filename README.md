# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
```
import socket
import webbrowser
import os

def send_request(host, port, request):

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:

        s.connect((host, port))

        s.sendall(request.encode())

        response = b""

        while True:

            data = s.recv(4096)

            if not data:
                break

            response += data

    return response.decode(errors="ignore")

def download_and_open(host, port):

    request = (
        f"GET / HTTP/1.1\r\n"
        f"Host: {host}\r\n"
        f"Connection: close\r\n\r\n"
    )

    response = send_request(host, port, request)

    html_content = """
    <html>
    <head>
        <title>Web Page</title>
    </head>

    <body style="background-color: lightblue; text-align: center; font-family: Arial, sans-serif;">
        <h1 style="color: yellow;">Welcome to my webpage</h1>
        <h2 style="color: red;">Danaseelan G[212225040053]</h2>
    </body>
    <button style="
        background-color: green;
        color: white;
        font-size: 20px;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;">

        Click Me

    </button>

    </html>
    """

    filename = "page.html"

    with open(filename, "w", encoding="utf-8") as f:
        f.write(html_content)

    print("HTML page saved.")
    print("Opened in browser.")

    path = os.path.abspath(filename)

    webbrowser.open("file://" + path)

if __name__ == "__main__":

    host = "example.com"
    port = 80

    download_and_open(host, port)

```
## OUTPUT
<img width="1920" height="1022" alt="image" src="https://github.com/user-attachments/assets/838753c8-7d36-4249-821c-2d666dfff980" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
