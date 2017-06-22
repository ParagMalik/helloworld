//# helloworld
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.SqlClient;
using System.Configuration;
using System.Data;

/// <summary>
/// Summary description for Class2
/// </summary>
public class Class2
{
    SqlCommand cmd;
    public SqlConnection con;
    SqlDataReader dr;
	public Class2()
	{

        con = new SqlConnection(ConfigurationManager.ConnectionStrings["KRPTest"].ToString());//
		// TODO: Add constructor logic here
		//
	}
    public DataTable select(string s)
    {
        DataTable dt = new DataTable();
        try
        {
            con.Open();
            cmd = new SqlCommand(s, con);
            dr = cmd.ExecuteReader();

            dt.Load(dr);

        }
        catch (Exception)
        {
        }
        con.Close();
        return dt;
    }
    public string insert(string s, SqlParameter[] sp)
    {
        string msg;
        try
        {


            con.Open();
            cmd = new SqlCommand(s, con);
            for (int i = 0; i < sp.Length; i++)
            {
                cmd.Parameters.Add(sp[i]);
            }
            cmd.ExecuteNonQuery();

            con.Close();
            msg = "success";
        }
        catch (Exception e)
        {
            msg = e.Message;
            con.Close();
        }
        return msg;
    }
    public DataTable select2(string s, SqlParameter[] sp)
    {
        DataTable dt = new DataTable();
        try
        {

            con.Open();
            cmd = new SqlCommand(s, con);
            for (int i = 0; i < sp.Length; i++)
            {
                cmd.Parameters.Add(sp[i]);
            }

            dr = cmd.ExecuteReader();

            dt.Load(dr);



        }
        catch (Exception)
        {


        }
        con.Close();
        return dt;
    }
}
