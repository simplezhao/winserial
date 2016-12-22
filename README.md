# winserial
windows系统下串口的使用
主要函数：
1. 初始化串口函数（端口，波特率，停止位，校验位）
`openSerialPort(portname,audrate baudrate, Stopbits stopbits, Paritycheck parity);`
2. 向串口写数据（File HANDLE，数据，长度）
`writeToSerialPort(hSerial, data, length);`
3. 从串口中读取数据（File HANDLE，buff，长度）
`readFromSerialPort(hSerial, buffer, buffersize);`
4. 关闭串口
`closeSerialPort(hSerial);`

下面是一个sample:
```
#include <stdio.h>
#include <stdlib.h>
#include "serialport.h"
int main(void)
{
	HANDLE h = openSerialPort("COM4",B115200,one,off);
	char at[] = "hello world\r\n";
	char readbuffer[1024];
	int bytesRead;
	/*把数据发送至串口*/
	writeToSerialPort(h,at,strlen(at));
	/*阻塞式，等待接收到数据*/
	bytesRead = readFromSerialPort(h,readbuffer,1024);
	readbuffer[bytesRead]='\0';
	printf("%s\n",readbuffer);
	/*关闭串口*/
	closeSerialPort(h);
	return 0;
}

```
