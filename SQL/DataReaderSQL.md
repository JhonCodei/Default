using System;
using System.Data.SqlClient;

namespace @@NAMESPACE__DATAREADERSQL
{
    public class DataReaderSQL
    {
        public static bool _HasColumn(SqlDataReader drd, String campo)
        {
            try
            {
                return drd.GetOrdinal(campo) >= 0;
            }
            catch (Exception ex)
            {
                _ = ex.Message;
                return false;
            }
        }
    }
}
