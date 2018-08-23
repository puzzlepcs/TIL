# JDBC
![img01](http://github.com/puzzlepcs/TIL/master/blob/Java/img/jdbc01.PNG)

## JDBC 실행절차
1. JDBC driver 등록
2. Driver Manager의 getConnection()를 이용해서 Connection 객체 얻어내기
3. Connection 객체의 createStatement()를 이용해서 Statement객체 얻어내기
4. Statement객체의 executeQuery()나 executeUpdate()를 이용해서 SQL을 DB에 전송
5. ResultSet 객체의 getXXX()를 이용 SQL문장의 실행결과 얻기
6. Statement객체와 Connection객체의 close()호출해서 connection 닫기

## 예제
```
public class JdbcOracleAll{

public static void main(String args[]) {
  String url = "jdbc:oracle:thin:@localhost:1521:xe";
  String user = "scott";
  String passwd = "tiger";

  Connection conn;
  Statement stat;
  try {
    // 1. JDBC driver
    Class.forName("oracle.jdbc.driver.OracleDriver");

    // 2. get connection instance
    conn = DriverManager.getConnection (url, user, passwd);

    // 3. create Statement(an object that can carry a query)
    stat = conn.createStatement();

    // 4. query
    String q = "select * from addressBook order by id";
    ResultSet rs = stat.executeQuery(q);

    // 5. get result
    while(rs.next()) {
      String id = rs.getString(1);
      String name = rs.getString(2);
      String phone = rs.getString(3);
      String address = rs.getString(4);
      String company = rs.getString(5);
      System.out.println(id + "|" + name + "\t|" + phone + "\t|" + address + "\t|" + company);
    }

    stat.close();
    conn.close();
  } catch ( Exception e ) {			
    e.printStackTrace();
  }
}
}
```
