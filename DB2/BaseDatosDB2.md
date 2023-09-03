using System;
using IBM.Data.DB2;

namespace @@NAMESPACE__HELPER_BASEDATOSDB2
{
    public class BaseDatosDB2
    {
        public DB2Connection Conexion;
        public bool EstaConectado = false;

        public DB2Transaction Transaccion;
        public bool EsTransaccion = false;

        public static String ConnectionString
        {
            get { return dllIQF_Settings.dll.ConnectionStrings.DB2_IQFARMA; }
        }

        public bool Conectar()
        {
            this.Conexion = new DB2Connection(ConnectionString);
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

