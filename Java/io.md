# Java I/O
## 1. Node Stream
![img01](https://github.com/puzzlepcs/TIL/blob/master/Java/img/io01.PNG)  
java는 bytestream처리에 특화되어 있다.
따라서 다음 코드는 잘 사용되지 않는다.
node stream으로 하면 기능도 적고 느리다는 단점이 있다.

## 2. Processing Stream
![img02](https://github.com/puzzlepcs/TIL/blob/master/Java/img/io02.PNG)  
원하는 기능을 추가.
byte stream -> char stream (InputStreamReader,OutputStreamWriter) : bytestream is faster than char stream.

byte stream reads the file by 1 byte.
if input type is int, have to read 4 bytes each time. ->

기능|CharacterStream|Bytestream
---|---|---
Buffering|BufferedReader, BufferedWriter | BufferedInputStream, BufferedOutputStream
Filtering|FilterReader, FilterWriter|FilterInpuStream, FilterOutputStream
Converting(byte character)|InputStreamReader, OutputStreamWriter|
Object Serialization| | ObjectIputStream, ObjectOutputStream
Data Conversion| | DataInputStream, DataOutputStream
Counting|LineNumberReader| LineNumberInputStream
Peeking ahead|PushbackReader|PushvackInputStream
Printing|PrintWriter|PrintStream


## 3. 객체를 파일에 입출력하기
markinterface -> java.io.Serializable 임터페이스를 implement하고 있는 클래스는 직렬화할 수 있다.
Customer에게 직렬화할 수 있는 클래스임을 명시해줌.
```
public class Customer  implements java.io.Serializable
{
	String  name;
	String  address;
	transient int	    age;

	public String toString(){
		return "이름 : "+name+"\t주소 : "+address+"\t나이 : "+age;
	}
}
```

여기서 `transient`키워드는 Serialize되지 않는 필드라는 것을 명시해 준다.
