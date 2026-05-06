server.py

import socket
import threading

clients = []

def broadcast(message, sender_conn):
    for client in clients:
        if client != sender_conn:
            try:
                client.send(message)
            except:
                clients.remove(client)

def handle_client(conn, addr):
    print(f"✅ New connection: {addr}")
    while True:
        try:
            message = conn.recv(1024)
            if not message:
                break
            broadcast(message, conn)
        except:
            break

    print(f"❌ Connection closed: {addr}")
    clients.remove(conn)
    conn.close()

def start_server():
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(("0.0.0.0", 9999))   # host, port
    server.listen(2)

    print("🚀 Server started on port 9999...")
    print("Waiting for clients to connect...\n")

    while True:
        conn, addr = server.accept()
        clients.append(conn)

        thread = threading.Thread(target=handle_client, args=(conn, addr))
        thread.start()

start_server()




client.py


import socket
import threading

def receive_messages(client):
    while True:
        try:
            message = client.recv(1024).decode()
            if message:
                print("\nFriend:", message)
        except:
            print("❌ Disconnected from server.")
            break

def send_messages(client):
    while True:
        message = input("You: ")
        client.send(message.encode())

def start_client():
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    server_ip = input("Enter Server IP Address: ")
    client.connect((server_ip, 9999))

    print("✅ Connected to chat server!")
    print("Start chatting...\n")

    thread = threading.Thread(target=receive_messages, args=(client,))
    thread.start()

    send_messages(client)

start_client()

