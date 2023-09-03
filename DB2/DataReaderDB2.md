using System;
using IBM.Data.DB2;

namespace @@NAMESPACE__DATAREADERDB2
{
    public class DataReaderDB2
    {
        public static bool _HasColumn(DB2DataReader drd, String campo)
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
