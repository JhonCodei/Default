using System;

namespace @@NAMESPACE__HELPER_BASEDATOSSQL
{
    public class BaseDatosSQL
    {
        public System.Data.SqlClient.SqlConnection Conexion;
        public bool EstaConectado = false;

        public System.Data.SqlClient.SqlTransaction Transaccion;
        public bool EsTransaccion = false;

        public static String ConnectionString
        {
            get { return dllIQF_Settings.dll.ConnectionStrings.SQL_dbsIQFarma; }
        }

        public bool Conectar()
        {
            this.Conexion = new System.Data.SqlClient.SqlConnection(ConnectionString);
            this.Conexion.Open();

            this.EstaConectado = true;
            return true;
        }

        public bool Desconectar()
        {
            if (this.Conexion.State == System.Data.ConnectionState.Open) { this.Conexion.Close(); }
            if (this.Conexion != null) { this.Conexion.Dispose(); }
            this.EstaConectado = false;
            return true;
        }

        public bool IniciarTransaccion()
        {
            this.Transaccion = this.Conexion.BeginTransaction();
            this.EsTransaccion = true;
            return true;
        }

        public bool CompletarTransaccion()
        {
            this.Transaccion.Commit();
            this.EsTransaccion = false;
            return true;
        }

        public bool CancelarTransaccion()
        {
            this.Transaccion.Rollback();
            this.EsTransaccion = false;
            return true;
        }
    }
}

