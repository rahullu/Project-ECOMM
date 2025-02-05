import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MultiDatabaseConnection {

    // Method to get connection to Azure SQL Database
    public static Connection getAzureSQLConnection() throws SQLException {
        String url = "jdbc:sqlserver://<your-azure-sql-server>.database.windows.net:1433;database=<your-database-name>";
        String user = "<your-username>";
        String password = "<your-password>";

        return DriverManager.getConnection(url, user, password);
    }

    // Method to get connection to MySQL Database
    public static Connection getMySQLConnection() throws SQLException {
        String url = "jdbc:mysql://<your-mysql-server>:3306/<your-database-name>";
        String user = "<your-username>";
        String password = "<your-password>";

        return DriverManager.getConnection(url, user, password);
    }

    public static void main(String[] args) {
        Connection azureSQLConnection = null;
        Connection mySQLConnection = null;

        try {
            // Establish connection to Azure SQL Database
            azureSQLConnection = getAzureSQLConnection();
            System.out.println("Connected to Azure SQL Database successfully.");

            // Establish connection to MySQL Database
            mySQLConnection = getMySQLConnection();
            System.out.println("Connected to MySQL Database successfully.");

            // Your database operations here...

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // Close the connections
            try {
                if (azureSQLConnection != null && !azureSQLConnection.isClosed()) {
                    azureSQLConnection.close();
                }
                if (mySQLConnection != null && !mySQLConnection.isClosed()) {
                    mySQLConnection.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
