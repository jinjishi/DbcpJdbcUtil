# DbcpJdbcUtil
package intership2.dao;
import org.apache.commons.dbcp2.BasicDataSourceFactory;
import javax.sql.DataSource;
import java.sql.ResultSet;
import java.sql.Statement;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;
public class DbcpJdbcUtil{
	private static DataSource ds = null;
	static {
		try {
			InputStream in = DbcpJdbcUtil.class.getClassLoader().getResourceAsStream("dbcp.properties");
			Properties prop = new Properties();
			prop.load(in);
			ds = BasicDataSourceFactory.createDataSource(prop);
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
public static Connection getConnection() throws SQLException{
	return ds.getConnection();
}
public static void release(Connection conn, Statement st, ResultSet rs) {
	if (rs !=null) {
		try {
			rs.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	if (st !=null) {
		try {
			st.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	if(conn !=null) {
		try {
			conn.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
}
}
