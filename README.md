# baiKT

Ketnoi
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package Model;

import java.sql.*;
import java.sql.Connection;
import java.sql.SQLException;
import java.sql.DriverManager;

/**
 *
 * @author Admin
 */
public class Conn {

    protected Connection cnn;

    public Conn() {
        try {
            String url = "jdbc:sqlserver://localhost:1433;databaseName=QuanLySP;trustServerCertificate=true;encrypt=false";
            String user = "sa";
            String pass = "123456";
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            cnn = DriverManager.getConnection(url, user, pass);

        } catch (ClassNotFoundException | SQLException e) {
        }
    }
}

#### xuli
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package Model;
import java.sql.*;
import java.util.List;
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;
/**
 *
 * @author coc
 */
public class XulyTapChi {
    private Tapchi tc;

    public XulyTapChi() {
    }

    public Tapchi getTc() {
        return tc;
    }

    public void setTc(Tapchi tc) {
        this.tc = tc;
    }

    public XulyTapChi(Tapchi tc) {
        this.tc = tc;
    }
    public List<Tapchi> getAllTapchi(){
        List<Tapchi> dstapchi = new ArrayList<>();
        String query ="select * from tapchi";
        try {
            Statement stm = Conn.getConnect().createStatement();
            ResultSet rs = stm.executeQuery(query);
            while(rs.next()){
                Tapchi tc = new Tapchi(rs.getString(1),rs.getString(2),rs.getString(3),Integer.parseInt(rs.getString(4)));
                dstapchi.add(tc);
            }
        } catch (SQLException ex) {
            Logger.getLogger(XulyTapChi.class.getName()).log(Level.SEVERE, null, ex);
        }
        return dstapchi;
    }
    
    public boolean themTapchi(){
        String query = "insert into Tapchi() values (?,?,?,?)";
        try {
            PreparedStatement pstm = Conn.getConnect().prepareStatement(query);
            pstm.setString(1, this.tc.getMaTC());
            pstm.setString(1, this.tc.getTenTC());
            pstm.setString(1, this.tc.getNhaXB());
            pstm.setInt(1, this.tc.getNamXB());
            return pstm.execute();
        } catch (SQLException ex) {
            Logger.getLogger(XulyTapChi.class.getName()).log(Level.SEVERE, null, ex);
        }
        return false;
    }
}
