using System;
using System.Collections;
using System.Collections.Generic;
using System.Net;
using System.Net.Sockets;
using System.Text;
using UnityEngine;

public class SocketControler : MonoBehaviour {

	// Use this for initialization
	void Start () {

        const int bufferSize = 8792;//缓存大小,8192字节  
        IPAddress ip = IPAddress.Parse("192.168.0.13");

        TcpListener tlistener = new TcpListener(ip, 10001);
        tlistener.Start();
        Console.WriteLine("服务器监听启动......");
        TcpClient remoteClient = tlistener.AcceptTcpClient();//接收已连接的客户端,阻塞方法  
        Console.WriteLine("客户端已连接！local:{0}<---Client:{1}", remoteClient.Client.LocalEndPoint, remoteClient.Client.RemoteEndPoint);

        //接收客户端发送的数据部分  
        NetworkStream streamToClient = remoteClient.GetStream();//获得来自客户端的流  
        byte[] buffer = new byte[bufferSize];//定义一个缓存buffer数组  
        int byteRead = streamToClient.Read(buffer, 0, bufferSize);//将数据搞入缓存中（有朋友说read是阻塞方法，测试中未发现程序阻塞）  
        string msg = Encoding.Unicode.GetString(buffer, 0, byteRead);//从二进制转换为字符串对应的客户端会有从字符串转换为二进制的方法  
        Console.WriteLine("接收数据：{0}[{1}byte]", msg, byteRead);

        //ConsoleKey key;
        //do
        //{
        //    key = Console.ReadKey(true).Key;
        //}
        //while (key != ConsoleKey.Q);

    }
	
	// Update is called once per frame
	void Update () {
		
	}
}
