LINK DESCARGA: https://drive.google.com/file/d/16ZwT2iTlIbiarfI7VGMgue5K2Ttx0RqM/view?usp=sharing
# Cajero-Automatico-Java-
Uso y manipulacion de archivos y documentos de texto, tambien de forma grafica
Modo de uso:
las direcciones empiezan con "C://etc,cuenta o tarjeta"+"variable"+".txt"
se debe reemplazar todo lo que esta antes de "variable" para el correcto funcionamiento del programa para ver la direccion de la carpeta selecciona el archivo descargado ve a propiedades copia la direccion de la carpetas "cuentas" o "tarjetas"
Ejemplo: 
"Donde guardaste el proyecto\\cuentas\\" + cuenta + ".txt")
"Donde guardaste el proyecto\\tarjetas\\" + tarjeta + ".txt")
"C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuentaADepositar+".txt"
"C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\"+tarjeta+".txt"
--------------------------------------------------------------------------------------------

Clases con direcciones: 
CambioMoneda
OtroMonto
OtroMontoI
SaldoCuentas
historial
inicio
menu
retiros
transaccionIII
OtraCuenta
CuentasBotones
--
--------------------------------------------------------------------------------------------
El trabajo de cajero automatico:

En este trabajo de vera la gran utilidad que tiene el uso y manejo de archivos y documentos de texto dentro de java e igualmente su uso grafico explicada para un uso practico y su utilidad para demas trabajos en el futuro.

Este problema tiene como objetivo tener las diferentes opciones:
*Poder tener una tarjeta de credito o debito con su respectivo pin
*Elegir a que cuenta se desea ingresar (estas pertenecientes a la misma tarjeta)
*Poder consultar el saldo de la cuenta con los ultimos 10 movimientos que realizo esta cuenta
*Ver en que moneda se encuentra la cuenta (sea bolivianos, dolares y euros)
*Ver el nombre del dueño de la tarjeta
*Poder depositar dinero
*Poder retirar dinero
*Poder transferir dinero entre cuentas 
*Poder cambiar de moneda 
*Cambiar el pin de la tarjeta

Todo esto desde el propio programa

Empezando por orden alfabetico con las clases:
Clase Cajero:
Esta es la menos relevante porque solo se encarga de llamar a la clase "inicio", ya que esta fue la primera en ser creada por lo tanto es la principal asi que dependiendo de la id que utilices si corres directo el programa la primera clase en ser llamada es esta.
package cajero; // Define el paquete donde se encuentra la clase.
//Clase Cajero---------------------------------------------------------------------------

/**
 * Clase principal para la aplicación del cajero automático.
 * 
 * @autor andres
 */
public class Cajero {

    /**
     * Método principal que se ejecuta al iniciar el programa.
     * 
     * @param args argumentos de línea de comandos (no utilizados en este caso)
     */
    public static void main(String[] args) {
        // Crea una instancia de la clase inicio
        inicio i = new inicio();
        
        // Hace visible la ventana de la interfaz gráfica del usuario (GUI)
        i.setVisible(true);
    }
    
}
//----------------------------------------------------------------------------------------

*Clase grafica Cambio de moneda

Esta clase sensillamente tiene 3 botones que lo que hace es como dice la clase cambiar de moneda, es decir si tu cuenta esta en dolares puedes cambiar entre 2 opciones mas sea euros o pesos bolivianos, el unico margen de "error" ya que no es un error como tal es una opcion es que eligas tu propia moneda, es decir si tu cuenta esta en dolares y eliges dolares te saltara un mensaje de que su cuenta ya se encuentra en dolares o de la moneda en la que se encuentre su cuenta:


//Clase CambioMoneda----------------------------------------------------------- 


package cajero;

import java.awt.Graphics; // Importa la clase Graphics para dibujar en componentes.
import java.awt.Image; // Importa la clase Image para manejar imágenes.
import javax.swing.Icon; // Importa la interfaz Icon para representar iconos.
import javax.swing.ImageIcon; // Importa la clase ImageIcon para manejar iconos de imagen.
import javax.swing.JButton; // Importa la clase JButton para usar botones en la interfaz.
import javax.swing.JOptionPane; // Importa la clase JOptionPane para mostrar cuadros de diálogo.
import javax.swing.JPanel; // Importa la clase JPanel para manejar paneles de contenido.



/**
 * Clase para la interfaz de cambio de moneda.
 * @author andres
 */
public class CambioMoneda extends javax.swing.JFrame {
public Fondo imagen = new Fondo(); // Instancia de la clase Fondo para establecer la imagen de fondo
    static String cuenta; // Variable estática para almacenar la cuenta
    static String tarjeta; // Variable estática para almacenar la tarjeta
    CambiosEnSaldo camb = new CambiosEnSaldo(); // Instancia para manejar cambios en el saldo
    funcionalidad fun = new funcionalidad(); // Instancia para manejar funcionalidades adicionales

  /**
   * Constructor de la clase.
   * @param cuenta La cuenta del usuario.
   * @param tarjeta La tarjeta del usuario.
   */
  public CambioMoneda(String cuenta, String tarjeta) {
    this.cuenta = cuenta;
    this.tarjeta = tarjeta;
    this.setContentPane(imagen); // Establece la imagen de fondo
        initComponents();
        setResizable(false); // Deshabilita la capacidad de redimensionar la ventana
        
    
    // Configuración de los íconos de los botones
    dolar1.setIcon(setIcono("/imagenes/dolar.png", dolar1));
    dolar1.setPressedIcon(setIconoPrecionado("/imagenes/dolar.png", dolar1, 30, 30));
    
    euro1.setIcon(setIcono("/imagenes/euro.png", euro1));
    euro1.setPressedIcon(setIconoPrecionado("/imagenes/euro.png", euro1, 30, 30));
    
    bol1.setIcon(setIcono("/imagenes/bol.png", bol1));
    bol1.setPressedIcon(setIconoPrecionado("/imagenes/bol.png", bol1, 30, 30));
  }

  @SuppressWarnings("unchecked")
  // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
  private void initComponents() {
    // Esta función ha sido omitida por que es parte del propio IDE y no es modificable.
  }                        

  /**
   * Acción cuando se presiona el botón euro1.
   * @param evt Evento de acción.
   */


  private void euro1ActionPerformed(java.awt.event.ActionEvent evt) {                                      
    // Verificación del tipo de moneda de la cuenta llamando a otras clases para poder manipular los datos de la cuenta
    boolean euros = camb.lineaContieneEu("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean bolivianos = camb.lineaContieneBs("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean dolares = camb.lineaContieneDlr("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    double saldo = fun.leerSaldo("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");

    if (euros) {
      // Si ya está en euros te manda al menu principal 
      JOptionPane.showMessageDialog(null, "SU CUENTA YA SE ENCUENTRA EN EUROS!!");//Salto del mensaje de "Error"
      menu v = new menu(tarjeta, cuenta);//Instancia para el menu Principal
      v.setVisible(true);//Abrir el menu principal
      dispose();//Cerrar la ventana actual
    } else if (bolivianos) {
      // Convertir de bolivianos a euros
      double nuevoSaldo = camb.bolivianosAEuros(saldo);
      camb.reemplazarEuPorBs("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE BOLIVIANOS A EUROS: BS*0.13");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    } else if (dolares) {
      // Convertir de dólares a euros
      double nuevoSaldo = camb.dolaresAEuros(saldo);
      camb.reemplazarEuPorDlr("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE DOLARES A EUROS: DLRS * 0.85");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    }
  }                                     

  /**
   * Acción cuando se presiona el botón bol1.
   * @param evt Evento de acción.
   */
  private void bol1ActionPerformed(java.awt.event.ActionEvent evt) {                                     
    // Verificación del tipo de moneda de la cuenta
    boolean euros = camb.lineaContieneEu("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean boliviano = camb.lineaContieneBs("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean dolares = camb.lineaContieneDlr("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    double saldo = fun.leerSaldo("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");

    if (boliviano) {
      // Si ya está en bolivianos
      JOptionPane.showMessageDialog(null, "SU CUENTA YA SE ENCUENTRA EN BOLIVIANOS!!");
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    } else if (dolares) {
      // Convertir de dólares a bolivianos
      double nuevoSaldo = camb.dolaresABolivianos(saldo);
      camb.reemplazarBsPorDlr("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE DOLARES A BOLIVIANOS: DLRS*6.89655");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    } else if (euros) {
      // Convertir de euros a bolivianos
      double nuevoSaldo = camb.eurosABolivianos(saldo);
      camb.reemplazarBsPorEu("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE EUROS A BOLIVIANOS: EU * 7.52");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    }
  }                                    

  /**
   * Acción cuando se presiona el botón dolar1.
   * @param evt Evento de acción.
   */
  private void dolar1ActionPerformed(java.awt.event.ActionEvent evt) {                                       
    // Verificación del tipo de moneda de la cuenta
    boolean euros = camb.lineaContieneEu("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean bolivianos = camb.lineaContieneBs("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    boolean dolares = camb.lineaContieneDlr("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");
    double saldo = fun.leerSaldo("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt");

    if (dolares) {
      // Si ya está en dólares
      JOptionPane.showMessageDialog(null, "SU CUENTA YA SE ENCUENTRA EN DOLARES!!");
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    } else if (bolivianos) {
      // Convertir de bolivianos a dólares
      double nuevoSaldo = camb.bolivianosADolares(saldo);
      camb.reemplazarDlrPorBs("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE BOLIVIANOS A DOLARES: BS *0.145");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    } else if (euros) {
      // Convertir de euros a dólares
      double nuevoSaldo = camb.eurosADolares(saldo);
      camb.reemplazarDlrPorEu("Donde guardaste el proyecto\\cajero\\cuentas\\" + cuenta + ".txt", nuevoSaldo);
      JOptionPane.showMessageDialog(null, "OPERACION REALIZADA CON EXITO");
      historial his = new historial(cuenta, "SE CAMBIO DE EUROS A DOLARES: EU *1.18");
      his.guardar();
      menu v = new menu(tarjeta, cuenta);
      v.setVisible(true);
      dispose();
    }
  }                                      

//Esta parte es propia del IDE y no es modificable

  /**
   * Clase principal.
   * @param args Argumentos de línea de comandos.
   */
  public static void main(String args[]) {
    /* Set the Nimbus look and feel */
    //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
    /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
     * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
     */
    try {
      for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
        if ("Nimbus".equals(info.getName())) {
          javax.swing.UIManager.setLookAndFeel(info.getClassName());
          break;
        }
      }
    } catch (ClassNotFoundException ex) {
      java.util.logging.Logger.getLogger(CambioMoneda.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (InstantiationException ex) {
      java.util.logging.Logger.getLogger(CambioMoneda.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (IllegalAccessException ex) {
      java.util.logging.Logger.getLogger(CambioMoneda.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (javax.swing.UnsupportedLookAndFeelException ex) {
      java.util.logging.Logger.getLogger(CambioMoneda.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    }
    //</editor-fold>

    /* Create and display the form */
    java.awt.EventQueue.invokeLater(new Runnable() {
      public void run() {
        new CambioMoneda(cuenta, tarjeta).setVisible(true);
      }
    });
  }

  // Variables declaration - do not modify                     
  private javax.swing.JButton bol1;
  private javax.swing.JButton dolar1;
  private javax.swing.JButton euro1;
  private javax.swing.JLabel imagen2;
  private javax.swing.JLabel texto2;
  // End of variables declaration                   

  /**
   * Método para establecer el icono de un botón.
   * @param path Ruta del icono.
   * @param boton Botón al que se le asignará el icono.
   * @return Icono para el botón.
   */
  private Icon setIcono(String path, JButton boton) {
    ImageIcon icon = new ImageIcon(getClass().getResource(path));
    int width = boton.getWidth();
    int height = boton.getHeight();
    Image img = icon.getImage().getScaledInstance(width, height, Image.SCALE_SMOOTH);
    return new ImageIcon(img);
  }

  /**
   * Método para establecer el icono presionado de un botón.
   * @param path Ruta del icono.
   * @param boton Botón al que se le asignará el icono.
   * @param ancho Ancho del icono.
   * @param alto Alto del icono.
   * @return Icono presionado para el botón.
   */
  private Icon setIconoPrecionado(String path, JButton boton, int ancho, int alto) {
    ImageIcon icon = new ImageIcon(getClass().getResource(path));
    Image img = icon.getImage().getScaledInstance(ancho, alto, Image.SCALE_SMOOTH);
    return new ImageIcon(img);
  }

  /**
   * Clase interna para el fondo de la ventana.
   */
  class Fondo extends JPanel {
    private Image img;

    /**
     * Sobrescribir el método paint para dibujar el fondo.
     * @param g Objeto Graphics.
     */
    @Override
    public void paint(Graphics g) {
      img = new ImageIcon(getClass().getResource("/imagenes/fondo1.png")).getImage();
      g.drawImage(img, 0, 0, getWidth(), getHeight(), this);
      setOpaque(false);
      super.paint(g);
    }
  }
}

//Fin---------------------------------------------------------------------------------------

*CambiosEnSaldo

Esta clase es mucho muy importante porque lo que hace es dar funcionalidad a otras clases ya que esta clase no es grafica solo contiene funciones.


//Clase CambiosEnSaldo--------------------------------------------------------------------------
package cajero; // Define el paquete al que pertenece esta clase.

import java.io.BufferedReader; // Importa la clase BufferedReader para leer texto de un flujo de entrada.
import java.io.BufferedWriter; // Importa la clase BufferedWriter para escribir texto a un flujo de salida.
import java.io.File; // Importa la clase File para manejar archivos y directorios.
import java.io.FileReader; // Importa la clase FileReader para leer archivos.
import java.io.FileWriter; // Importa la clase FileWriter para escribir archivos.
import java.io.IOException; // Importa la clase IOException para manejar excepciones de E/S.
import javax.swing.JOptionPane; // Importa la clase JOptionPane para mostrar cuadros de diálogo.

/**
 * Clase CambiosEnSaldo.
 * Esta clase proporciona funciones para verificar cuentas y realizar transferencias de dinero.
 * @autor fband
 */

// Definición de la clase CambiosEnSaldo.
public class CambiosEnSaldo {
    
    // Método para verificar si un archivo de cuenta existe.
    public boolean verificarCuenta(String rutaArchivo) {
        File archivo = new File(rutaArchivo); // Crea un objeto File con la ruta del archivo.
        return archivo.exists(); // Retorna true si el archivo existe, false en caso contrario.
    }
    
    // Método para verificar si una misma cuenta existe.
    public boolean verificarMisma(String rutaArchivo) {
        File archivo = new File(rutaArchivo); // Crea un objeto File con la ruta del archivo.
        return archivo.exists(); // Retorna true si el archivo existe, false en caso contrario.
    }
    
    // Método para verificar si dos archivos tienen la misma moneda.
    public boolean verificarMonedaCoin(String filePath1, String filePath2) {
        try (BufferedReader br1 = new BufferedReader(new FileReader(filePath1)); // Crea BufferedReader para leer el primer archivo.
             BufferedReader br2 = new BufferedReader(new FileReader(filePath2))) { // Crea BufferedReader para leer el segundo archivo.
             
            String linea1 = br1.readLine(); // Lee la primera línea del primer archivo.
            String linea2 = br2.readLine(); // Lee la primera línea del segundo archivo.

            if (linea1 == null || linea2 == null) {
                return false; // Retorna false si uno de los archivos está vacío.
            }

            String prefix1 = obtenerPrefijo(linea1); // Obtiene el prefijo de la primera línea del primer archivo.
            String prefix2 = obtenerPrefijo(linea2); // Obtiene el prefijo de la primera línea del segundo archivo.
            System.out.println(prefix1 + " " + prefix2); // Imprime los prefijos.

            return prefix1.equals(prefix2); // Retorna true si los prefijos son iguales, false en caso contrario.

        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
            return false; // Retorna false en caso de excepción.
        }
    }

    // Método privado para obtener el prefijo de una línea.
    private static String obtenerPrefijo(String linea) {
        int index = linea.indexOf(':'); // Encuentra el índice del carácter ':'.
        if (index == -1) {
            return ""; // Retorna una cadena vacía si no hay ':'.
        }
        return linea.substring(0, index).trim(); // Retorna el prefijo, que es la parte de la línea antes de ':'.
    }
    
    // Método para transferir dinero entre cuentas.
    public void transferirDinero(String cuenta1, String cuenta2, double deposito, String cuentanumeral1, String cuentanumeral2) {
        // Variables para almacenar los saldos
        double saldoCuenta1 = 0;
        double saldoCuenta2 = 0;
        String prefixCuenta1 = "";
        String prefixCuenta2 = "";
        
        // Leer saldos de las cuentas
        try (BufferedReader br1 = new BufferedReader(new FileReader(cuenta1)); // Crea BufferedReader para leer el archivo de la primera cuenta.
             BufferedReader br2 = new BufferedReader(new FileReader(cuenta2))) { // Crea BufferedReader para leer el archivo de la segunda cuenta.
            
            // Leer el saldo de cuenta1
            String linea1 = br1.readLine(); // Lee la primera línea del archivo de la primera cuenta.
            if (linea1 != null && linea1.contains(": ")) {
                prefixCuenta1 = linea1.substring(0, linea1.indexOf(": ") + 2); // Obtiene el prefijo "xx: ".
                saldoCuenta1 = Double.parseDouble(linea1.substring(linea1.indexOf(": ") + 2).trim()); // Obtiene el saldo.
            }
            
            // Leer el saldo de cuenta2
            String linea2 = br2.readLine(); // Lee la primera línea del archivo de la segunda cuenta.
            if (linea2 != null && linea2.contains(": ")) {
                prefixCuenta2 = linea2.substring(0, linea2.indexOf(": ") + 2); // Obtiene el prefijo "xx: ".
                saldoCuenta2 = Double.parseDouble(linea2.substring(linea2.indexOf(": ") + 2).trim()); // Obtiene el saldo.
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
            return;
        }
        
        // Verificar saldo suficiente en cuenta1
        if (saldoCuenta1 < deposito) {
            JOptionPane.showMessageDialog(null, "SALDO INSUFICIENTE", "Error", JOptionPane.ERROR_MESSAGE); // Muestra un mensaje de error.
            return; // Termina la función si el saldo es insuficiente.
        }
        
        // Decrementar el saldo de cuenta1 y sumar el depósito a cuenta2
        saldoCuenta1 -= deposito;
        saldoCuenta2 += deposito;

        // Guardar el historial de transacciones (esto es opcional y depende de tu implementación)
        historialTransacciones histT = new historialTransacciones(cuentanumeral1, cuentanumeral2, deposito); // Crea un objeto historialTransacciones.
        histT.guardarIngreso(); // Guarda el ingreso en el historial.
        histT.guardarDeposito(); // Guarda el depósito en el historial.
        
        // Escribir los nuevos saldos en los archivos
        try (BufferedWriter bw1 = new BufferedWriter(new FileWriter(cuenta1)); // Crea BufferedWriter para escribir en el archivo de la primera cuenta.
             BufferedWriter bw2 = new BufferedWriter(new FileWriter(cuenta2))) { // Crea BufferedWriter para escribir en el archivo de la segunda cuenta.
            
            bw1.write(prefixCuenta1 + saldoCuenta1); // Escribe el prefijo y el nuevo saldo en el archivo de la primera cuenta.
            bw1.newLine(); // Escribe una nueva línea.
            
            bw2.write(prefixCuenta2 + saldoCuenta2); // Escribe el prefijo y el nuevo saldo en el archivo de la segunda cuenta.
            bw2.newLine(); // Escribe una nueva línea.
            
            System.out.println("Transferencia exitosa."); // Imprime un mensaje de éxito.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }

    // Método para incrementar el saldo de una cuenta.
    public static void IncrementoSaldo(String nombreArchivo, double incremento) throws IOException {
        // Abrir el archivo para lectura
        try {
            File archivo = new File(nombreArchivo); // Crea un objeto File con la ruta del archivo.
            BufferedReader lector = new BufferedReader(new FileReader(archivo)); // Crea BufferedReader para leer el archivo.

            // Leer la primera línea y extraer el saldo
            String primeraLinea = lector.readLine(); // Lee la primera línea del archivo.
            double saldo = Double.parseDouble(primeraLinea.split(": ")[1]); // Obtiene el saldo.

            // Cerrar el lector
            lector.close(); // Cierra el BufferedReader.

            // Incrementar el saldo
            saldo += incremento; // Incrementa el saldo.
            
            // Abrir el archivo para escritura
            BufferedWriter escritor = new BufferedWriter(new FileWriter(archivo)); // Crea BufferedWriter para escribir en el archivo.

            // Escribir el nuevo saldo en el archivo
            escritor.write(primeraLinea.split(": ")[0] + ": " + saldo); // Escribe el nuevo saldo.

            // Cerrar el escritor
            escritor.close(); // Cierra el BufferedWriter.

            System.out.println("Saldo incrementado y actualizado en el archivo."); // Imprime un mensaje de éxito.
        } catch (IOException e) {
            System.err.println("Error de entrada/salida: " + e.getMessage()); // Imprime un mensaje de error.
        } catch (NumberFormatException | ArrayIndexOutOfBoundsException e) {
            System.err.println("Formato de archivo incorrecto."); // Imprime un mensaje de error.
        }
    }
        
    // Método para decrementar el saldo de una cuenta.
    public void DecrementoSaldo(String nombreArchivo, double decremento, String cuenta) {
        try {
            // Abrir el archivo para lectura
            File archivo = new File(nombreArchivo); // Crea un objeto File con la ruta del archivo.
            BufferedReader lector = new BufferedReader(new FileReader(archivo)); // Crea BufferedReader para leer el archivo.

            // Leer la primera línea y extraer el saldo
            String primeraLinea = lector.readLine(); // Lee la primera línea del archivo.
            double saldo = Double.parseDouble(primeraLinea.split(": ")[1]); // Obtiene el saldo.

            // Cerrar el lector
            lector.close(); // Cierra el BufferedReader.

            // Verificar si el decremento es mayor que el saldo actual
            if (decremento > saldo) {
                JOptionPane.showMessageDialog(null, "SALDO INSUFICIENTE"); // Muestra un mensaje de error.
                return; // Salir de la función si el decremento es mayor.
            }

            // Decrementar el saldo
            saldo -= decremento; // Decrementa el saldo.
            JOptionPane.showMessageDialog(null, "RETIRO REALIZADO CON EXITO"); // Muestra un mensaje de éxito.
            historial his = new historial(cuenta, "SE RETIRO DINERO: " + decremento); // Crea un objeto historial.
            his.guardar(); // Guarda el historial.

            // Abrir el archivo para escritura
            BufferedWriter escritor = new BufferedWriter(new FileWriter(archivo)); // Crea BufferedWriter para escribir en el archivo.

            // Escribir el nuevo saldo en el archivo
            escritor.write(primeraLinea.split(": ")[0] + ": " + saldo); // Escribe el nuevo saldo.

            // Cerrar el escritor
            escritor.close(); // Cierra el BufferedWriter.

            System.out.println("Saldo decrementado y actualizado en el archivo."); // Imprime un mensaje de éxito.
        } catch (IOException e) {
            System.err.println("Error de entrada/salida: " + e.getMessage()); // Imprime un mensaje de error.
        } catch (NumberFormatException | ArrayIndexOutOfBoundsException e) {
            System.err.println("Formato de archivo incorrecto."); // Imprime un mensaje de error.
        }
    }
    
    // Método para verificar si una línea en el archivo contiene "bs:".
    public boolean lineaContieneBs(String nombreArchivo) {
        try (BufferedReader br = new BufferedReader(new FileReader(nombreArchivo))) { // Crea BufferedReader para leer el archivo.
            String linea;
            while ((linea = br.readLine()) != null) {
                if (linea.contains("bs:")) {
                    return true; // Retorna true si la línea contiene "bs:".
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
        return false; // Retorna false si no se encuentra "bs:".
    }

    // Método para verificar si una línea en el archivo contiene "eu:".
    public boolean lineaContieneEu(String nombreArchivo) {
        try (BufferedReader br = new BufferedReader(new FileReader(nombreArchivo))) { // Crea BufferedReader para leer el archivo.
            String linea;
            while ((linea = br.readLine()) != null) {
                if (linea.contains("eu:")) {
                    return true; // Retorna true si la línea contiene "eu:".
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
        return false; // Retorna false si no se encuentra "eu:".
    }

    // Método para verificar si una línea en el archivo contiene "dlr:".
    public boolean lineaContieneDlr(String nombreArchivo) {
        try (BufferedReader br = new BufferedReader(new FileReader(nombreArchivo))) { // Crea BufferedReader para leer el archivo.
            String linea;
            while ((linea = br.readLine()) != null) {
                if (linea.contains("dlr:")) {
                    return true; // Retorna true si la línea contiene "dlr:".
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
        return false; // Retorna false si no se encuentra "dlr:".
    }
       
    // Función para convertir de bolivianos a dólares.
    public static double bolivianosADolares(double bolivianos) {
        return bolivianos * 0.145;
    }

    // Función para convertir de dólares a bolivianos.
    public static double dolaresABolivianos(double dolares) {
        return dolares * 6.89655;
    }

    // Función para convertir de bolivianos a euros.
    public static double bolivianosAEuros(double bolivianos) {
        return bolivianos * 0.13;
    }

    // Función para convertir de euros a bolivianos.
    public static double eurosABolivianos(double euros) {
        return euros * 7.52;
    }

    // Función para convertir de euros a dólares.
    public static double eurosADolares(double euros) {
        return euros * 1.18;
    }

    // Función para convertir de dólares a euros.
    public static double dolaresAEuros(double dolares) {
        return dolares * 0.85;
    }

    // Método para reemplazar "eu:" por "bs:" en un archivo.
    public static void reemplazarBsPorEu(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("eu:")) {
                    System.out.println("ok");
                    contenido.append("bs: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "eu:" por "bs:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }
    
    // Método para reemplazar "bs:" por "eu:" en un archivo.
    public static void reemplazarEuPorBs(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("bs:")) {
                    contenido.append("eu: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "bs:" por "eu:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }
    
    // Método para reemplazar "dlr:" por "bs:" en un archivo.
    public static void reemplazarBsPorDlr(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("dlr:")) {
                    contenido.append("bs: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "dlr:" por "bs:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }
    
    // Método para reemplazar "bs:" por "dlr:" en un archivo.
    public static void reemplazarDlrPorBs(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("bs:")) {
                    contenido.append("dlr: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "bs:" por "dlr:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }
    
    // Método para reemplazar "eu:" por "dlr:" en un archivo.
    public static void reemplazarDlrPorEu(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("eu:")) {
                    contenido.append("dlr: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "eu:" por "dlr:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }

    // Método para reemplazar "dlr:" por "eu:" en un archivo.
    public static void reemplazarEuPorDlr(String filePath, double nuevoContenido) {
        StringBuilder contenido = new StringBuilder();

        // Leer el archivo y reemplazar líneas en memoria
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) { // Crea BufferedReader para leer el archivo.
            String currentLine;
            while ((currentLine = reader.readLine()) != null) {
                if (currentLine.contains("dlr:")) {
                    contenido.append("eu: ").append(nuevoContenido).append(System.lineSeparator()); // Reemplaza "dlr:" por "eu:".
                } else {
                    contenido.append(currentLine).append(System.lineSeparator());
                }
            }
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }

        // Escribir el contenido actualizado de vuelta al archivo
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) { // Crea BufferedWriter para escribir en el archivo.
            writer.write(contenido.toString()); // Escribe el contenido actualizado.
        } catch (IOException e) {
            e.printStackTrace(); // Imprime la traza de la excepción.
        }
    }
}
//----------------------------------------------------------------------------------------------------------------------------------------

*Clase CuentasBotones:

Esta clase viene siendo una de las mas complejas ya que es grafica y dinamica, como?
Bueno esta clase lo que hace es leer un documento de texto y generar botones a concurrente con las lineas existentes dentro del documento de texto enviado:

Se comentara lo que es necesario de la propia clase ya que lo demas es propio del IDE y no es modificable.
//Clase CuentasBotones---------------------------------------------------------------------

package cajero;

// Importaciones necesarias para el funcionamiento del programa
import java.awt.Color;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JPanel;

/**
 * La clase CuentasBotones representa una ventana que muestra una serie de botones correspondientes a las cuentas
 * asociadas a una tarjeta específica.
 */
public class CuentasBotones extends javax.swing.JFrame {
    // La variable estática 'tarjeta' almacena el número de tarjeta actual.
    static String tarjeta;

    // Instancia de la clase Fondo para usarla como fondo de la ventana.
    public Fondo imagen = new Fondo(); 

    /**
     * Crea una nueva instancia de la clase CuentasBotones.
     * @param tarjeta El número de la tarjeta para la cual se muestran las cuentas.
     */
    public CuentasBotones(String tarjeta) {
        // Establece la posición de la ventana en el centro de la pantalla
        this.setLocationRelativeTo(null);
        // Asigna el número de tarjeta recibido como argumento a la variable 'tarjeta'
        this.tarjeta = tarjeta;
        // Inicializa los componentes de la interfaz gráfica
        initComponents();
        // Hace que la ventana no sea redimensionable
        setResizable(false);
        // Agrega los botones correspondientes a las cuentas de la tarjeta
        agregarBotonesPeliculas();
        // Ubica la ventana en el centro de la pantalla
        setLocationRelativeTo(null);
    }
    
    // Método privado para obtener las cuentas asociadas a la tarjeta actual
    private String[] obtenerCuentas(String tarjeta) {
        // Ruta del archivo que contiene las cuentas asociadas a la tarjeta
        String archivoPath = "C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjeta + ".txt";
        File archivo = new File(archivoPath);
        ArrayList<String> nCuentas = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(archivo))) {
            String linea;
            // Lee cada línea del archivo
            while ((linea = br.readLine()) != null) {
                // Si la línea no contiene ':', se asume que es el nombre de una cuenta
                if (!linea.contains(":")) {
                    nCuentas.add(linea);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        // Convierte el ArrayList a un array de Strings y lo devuelve
        return nCuentas.toArray(new String[0]);
    }

    // Método para agregar botones correspondientes a las cuentas en la interfaz gráfica
    private void agregarBotonesPeliculas() {
        // Obtiene las cuentas asociadas a la tarjeta actual
        String[] ncuentas = obtenerCuentas(tarjeta);
        // Itera sobre cada cuenta para crear un botón correspondiente
        for (String nombre : ncuentas) {
            JButton boton = new JButton(nombre);
            // Configura el botón con colores específicos
            configurarBotonConColor(boton, Color.RED, Color.WHITE);
            // Agrega un ActionListener al botón
            boton.addActionListener(new ActionListener() {
                @Override
                public void actionPerformed(ActionEvent e) {
                    // Cuando se hace clic en el botón, se guarda el nombre de la cuenta y se muestra el menú correspondiente
                    nncuentas = nombre;
                    menu pel = new menu(tarjeta, nncuentas);
                    pel.setVisible(true);
                    dispose();
                }
            });
            // Agrega el botón al panel de cuentas
            panelDeCuentas.add(boton);
        }
    }

    // Método para configurar un botón con colores específicos
    public void configurarBotonConColor(JButton boton, Color colorFondo, Color colorTexto) {
        boton.setBackground(colorFondo);
        boton.setForeground(colorTexto);
        boton.setFont(boton.getFont().deriveFont(java.awt.Font.BOLD, 42f)); // Establecer la fuente en negrita y tamaño 42
        boton.setOpaque(true);
        boton.setBorderPainted(false);  // Quitar el borde para que solo se vea el color de fondo
    }

//-----------------------------------------------------------------------------------------

*Clase OtraCuenta:

Esta clase grafica lo unico que tiene es un boton y una caja de texto que lo que hace es verificar la cuenta a la que intentas depositar:

Solo se comentara lo que es importante ya que lo demas es propio del IDE:

//Clase OtraCuenta-------------------------------------------------------------------------
package cajero;

// Importaciones necesarias para la interfaz gráfica y manipulación de imágenes
import java.awt.Graphics;
import java.awt.Image;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

/**
 * Clase que representa la ventana para realizar depósitos en otra cuenta.
 * Extiende de javax.swing.JFrame.
 */
public class OtraCuenta extends javax.swing.JFrame {
    
    // Variables estáticas para almacenar información sobre las cuentas y tarjetas
    static String cuenta;
    static String tarjeta;
    static String cuentaADepositar;
    
    // Instancia de Fondo para establecer el fondo de la ventana
    public Fondo imagen = new Fondo(); 
    
    /**
     * Constructor de la clase.
     * @param cuenta Número de cuenta actual.
     * @param tarjeta Número de tarjeta asociada a la cuenta.
     */
    public OtraCuenta(String cuenta, String tarjeta) {
        // Inicializa las variables de cuenta y tarjeta
        this.cuenta=cuenta;
        this.tarjeta=tarjeta;
        // Establece el contenido del panel como una instancia de Fondo
        this.setContentPane(imagen);
        // Inicializa los componentes de la interfaz gráfica
        initComponents();
        // Establece que la ventana no sea redimensionable
        setResizable(false);
        // Configura el botón de confirmar con un ícono y un ícono presionado
        confirmar.setIcon(setIcono("/imagenes/confirmar.png",confirmar));
        confirmar.setPressedIcon(setIconoPrecionado("/imagenes/confirmar.png",confirmar,30,30));
    }

    /**
     * Método generado automáticamente que inicializa los componentes de la interfaz gráfica.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {
        // Declaraciones de los componentes de la interfaz gráfica
        texto6 = new javax.swing.JLabel();
        texto1 = new javax.swing.JLabel();
        texto4 = new javax.swing.JLabel();
        numCuenta = new javax.swing.JTextField();
        confirmar = new javax.swing.JButton();
        imagen2 = new javax.swing.JLabel();
        texto5 = new javax.swing.JLabel();

        // Configuración de la ventana
        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        // Configuración de la etiqueta "texto6"
        texto6.setBackground(new java.awt.Color(51, 51, 51));
        texto6.setFont(new java.awt.Font("Arial Black", 3, 48)); // NOI18N
        texto6.setText("BNB");

        // Configuración de la etiqueta "texto1"
        texto1.setFont(new java.awt.Font("Arial Black", 3, 36)); // NOI18N
        texto1.setForeground(new java.awt.Color(0, 102, 153));
        texto1.setText("Ingrese el nro de la Cuenta");

        // Configuración de la etiqueta "texto4"
        texto4.setFont(new java.awt.Font("Arial Black", 3, 36)); // NOI18N
        texto4.setForeground(new java.awt.Color(0, 51, 102));
        texto4.setText("Ingrese  el  Nro de cuenta:");
        texto4.setToolTipText("");

        // Configuración del campo de texto "numCuenta"
        numCuenta.setBackground(new java.awt.Color(255, 204, 51));
        numCuenta.setFont(new java.awt.Font("Arial", 0, 24)); // NOI18N
        numCuenta.setHorizontalAlignment(javax.swing.JTextField.CENTER);
        numCuenta.setBorder(javax.swing.BorderFactory.createBevelBorder(javax.swing.border.BevelBorder.RAISED));

        // Configuración del botón "confirmar"
        confirmar.setBorderPainted(false);
        confirmar.setContentAreaFilled(false);
        confirmar.setFocusPainted(false);
        confirmar.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                confirmarActionPerformed(evt);
            }
        });

        // Configuración de la etiqueta "imagen2"
        imagen2.setIcon(new javax.swing.ImageIcon(getClass().getResource("/imagenes/logo1.png"))); // NOI18N

        // Configuración de la etiqueta "texto5"
        texto5.setFont(new java.awt.Font("Arial Black", 3, 36)); // NOI18N
        texto5.setForeground(new java.awt.Color(0, 51, 102));
        texto5.setText("(Depositar)");
        texto5.setToolTipText("");

        // Configuración del diseño de la ventana
        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(layout.createSequentialGroup()
                                .addContainerGap()
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                    .addComponent(texto4)
                                    .addGroup(layout.createSequentialGroup()
                                        .addComponent(texto6, javax.swing.GroupLayout.PREFERRED_SIZE, 152, javax.swing.GroupLayout.PREFERRED_SIZE)
                                        .addGap(628, 628, 628))))
                            .addGroup(layout.createSequentialGroup()
                                .addGap(74, 74, 74)
                                .addComponent(texto1)))
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addGap(0, 0, Short.MAX_VALUE)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                                .addComponent(confirmar, javax.swing.GroupLayout.PREFERRED_SIZE, 318, javax.swing.GroupLayout.PREFERRED_SIZE)
                                .addGap(201, 201, 201))
                            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                                .addComponent(texto5)
                                .addGap(238, 238, 238))
                            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                                .addComponent(numCuenta, javax.swing.GroupLayout.PREFERRED_SIZE, 543, javax.swing.GroupLayout.PREFERRED_SIZE)
                                .addGap(79, 79, 79)))))
                .addComponent(imagen2)
                .addContainerGap())
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(texto6)
                        .addGap(26, 26, 26)
                        .addComponent(texto1)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addComponent(texto5)
                        .addGap(53, 53, 53)
                        .addComponent(texto4)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addComponent(numCuenta, javax.swing.GroupLayout.PREFERRED_SIZE, 62, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(39, 39, 39)
                        .addComponent(confirmar, javax.swing.GroupLayout.PREFERRED_SIZE, 88, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGroup(layout.createSequentialGroup()
.addGap(54, 54, 54)
                        .addComponent(imagen2)))
                .addContainerGap(143, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    // Método para manejar la acción cuando se introduce un número de cuenta
    private void numCuentaActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // No se realiza ninguna acción específica en este caso
    }                                         

    // Método para manejar la acción cuando se presiona el botón de confirmar
    private void confirmarActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // Llama al método accionAlApretar()
        accionAlApretar();
    }                                         

    // Método para realizar acciones al presionar el botón de confirmar
    public void accionAlApretar(){
        // Instancia de CambiosEnSaldo para verificar cuentas y realizar transacciones
        CambiosEnSaldo cambios = new CambiosEnSaldo();
        // Obtiene el número de cuenta ingresado por el usuario
        cuentaADepositar = numCuenta.getText();
        // Verifica si la cuenta a la que se desea depositar existe
        boolean verificarExistencia =  cambios.verificarCuenta("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuentaADepositar+".txt");
        // Verifica si la moneda de la cuenta actual coincide con la moneda de la cuenta a depositar
        boolean verficarMoneda = cambios.verificarMonedaCoin("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt","C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuentaADepositar+".txt");  
        
        // Comienza a evaluar diferentes casos
        if(cuenta.equals(cuentaADepositar)){
            // Si la cuenta actual es la misma que la cuenta a depositar, muestra un mensaje de error
            JOptionPane.showMessageDialog(null, "ERROR AL INGRESAR LA CUENTA ES LA MISMA");
            // Crea una instancia de la ventana de menú y la muestra
            menu v = new menu(tarjeta,cuenta);
            v.setVisible(true);
            // Cierra la ventana actual
            dispose();
        } else {
            // Si la cuenta a depositar existe
            if(verificarExistencia){
                // Si la moneda coincide, crea una instancia de la ventana de transacción y la muestra
                if(verficarMoneda){
                    transaccionIII t = new transaccionIII(cuenta,tarjeta,cuentaADepositar);
                    t.setVisible(true);
                    // Cierra la ventana actual
                    dispose();
                } else {
                    // Si la moneda no coincide, muestra un mensaje de error
                    JOptionPane.showMessageDialog(null, "LAS MONEDA QUE USTED MANEJA NO COINCIDE CON LA CUENTA A LA QUE INTENTA DEPOSITAR"+"\n"+"FAVOR DE CAMBIAR DE MONEDA");
                    // Crea una instancia de la ventana de menú y la muestra
                    menu v = new menu(tarjeta,cuenta);
                    v.setVisible(true);
                    // Cierra la ventana actual
                    dispose();
                }
            } else {
                // Si la cuenta a depositar no existe, muestra un mensaje de error
                JOptionPane.showMessageDialog(null, "LA CUENTA A LA QUE INTENTA DEPOSITAR NO EXISTE!");
                // Crea una instancia de la ventana de menú y la muestra
                menu v = new menu(tarjeta,cuenta);
                v.setVisible(true);
                // Cierra la ventana actual
                dispose();
            }
        }
    }
    
    /**
     * Método principal de la clase.
     * @param args Los argumentos de la línea de comandos.
     */
    public static void main(String args[]) {
        // Configuración del aspecto de la interfaz gráfica
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(OtraCuenta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(OtraCuenta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(OtraCuenta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(OtraCuenta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        
        // Creación y visualización de la ventana
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                // Crea una instancia de OtraCuenta y la hace visible
                new OtraCuenta(cuenta,tarjeta).setVisible(true);
            }
        });
    }

class Fondo extends JPanel {

        private Image imagen;

        @Override
        public void paint(Graphics g) {
            imagen = new ImageIcon(getClass().getResource("/imagenes/fondo.png")).getImage();
            g.drawImage(imagen, 0, 0, getWidth(), getHeight(), this);
            setOpaque(false);
            super.paint(g);
        }
    }
     
     public Icon setIcono(String url,JButton b){
         ImageIcon  icon= new ImageIcon(getClass().getResource(url)); 
         int ancho =b.getWidth();
         int alto =b.getHeight();
         ImageIcon icono= new ImageIcon(icon.getImage().getScaledInstance(ancho,alto,Image.SCALE_DEFAULT)); 
         return icono;
     }
     public Icon setIconoPrecionado(String url,JButton b,int ancho,int alto){
       
         ImageIcon icon= new ImageIcon(getClass().getResource(url));
          int  width = b.getWidth()- ancho;
          int height = b.getHeight() - alto;
          ImageIcon icono = new ImageIcon(icon.getImage().getScaledInstance(width,height,Image.SCALE_DEFAULT));
          return icono;
     }
    // Variables declaration - do not modify                     
    private javax.swing.JButton confirmar;
    private javax.swing.JLabel imagen2;
    private javax.swing.JTextField numCuenta;
    private javax.swing.JLabel texto1;
    private javax.swing.JLabel texto4;
    private javax.swing.JLabel texto5;
    private javax.swing.JLabel texto6;
    // End of variables declaration                   
  }
//FIN-----------------------------------------------------------

*Clase OtroMonto

Esta clase sencillamente solo sirve para ingresar otro monto que se quiera retirar por lo tanto solo valdria la pena comentar 2 funciones:

//Clase Otromonto---------------------------------------------------------------------------
private void confirmarActionPerformed(java.awt.event.ActionEvent evt) {                                          
    // Llama al método para retirar el monto ingresado
    RetiroMonto();
}                                         

// Método para retirar el monto ingresado
public void RetiroMonto(){
    // Obtiene el monto ingresado desde el campo de texto
    String ingreso = numCuenta.getText();
    // Convierte el monto ingresado a un valor numérico (double)
    double dinero = Double.parseDouble(ingreso);
    
    //-----------------------------------------------------------------------------------------------------------
    // Llama al método para decrementar el saldo de la cuenta asociada a la tarjeta
    cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",dinero,cuenta);
    //----------------------------------------------------------------------------------------------------------
    
    // Crea una instancia de la clase "menu" y la hace visible, pasando los parámetros de la tarjeta y la cuenta
    menu i = new menu(tarjeta,cuenta);
    i.setVisible(true);
    // Cierra la ventana actual
    dispose(); 
}
//---------------------------------------------------------------------------------------------

*Clase OtroMontoI:

Como en la anterior clase no sirve de mucho comentar toda la clase solo vale la pena comentar 2 funciones, ya que lo unico que hace esta clase es ingresar el monto que se desea depositar a la cuenta propia:

//Clase OtroMontoI------------------------------------------------------------------------
private void confirmarActionPerformed(java.awt.event.ActionEvent evt) {                                          
    try {
        // Llama al método para realizar un depósito
        Deposito();
    } catch (IOException ex) {
        // Maneja cualquier excepción de E/S que pueda ocurrir al realizar el depósito
        Logger.getLogger(OtroMontoI.class.getName()).log(Level.SEVERE, null, ex);
    }
}                                         

// Método para realizar un depósito
public void Deposito() throws IOException{
    // Obtiene el monto ingresado desde el campo de texto
    String ingreso = numCuenta.getText();
    // Convierte el monto ingresado a un valor numérico (double)
    double dinero = Double.parseDouble(ingreso);
    
    //----------------------------------------------------------------------------------------------------------------------
    // Llama al método para incrementar el saldo de la cuenta asociada a la tarjeta
    cambio.IncrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",dinero);
    //----------------------------------------------------------------------------------------------------------------------
    
    // Muestra un mensaje de éxito al usuario
    JOptionPane.showMessageDialog(null, "ACCION REALIZADA CON EXITO");
    
    // Crea una instancia de la clase "historial" para registrar la acción de depósito en el historial de la cuenta
    historial his = new historial(cuenta,"SE  DEPOSITO DINERO"+" :"+dinero);
    // Guarda el registro en el historial
    his.guardar();
    
    // Abre una nueva instancia de la ventana de menú, pasando los parámetros de la tarjeta y la cuenta
    menu i = new menu(tarjeta,cuenta);
    i.setVisible(true);
    
    // Cierra la ventana actual
    dispose(); 
}
//FIN------------------------------------------------------------------------------------------------


*Clase SaldoCuentas:

Esta clase es muy importante por que aqui se muestra en que moneda se encuentra tu cuenta, tu saldo y el historial de los 10 ultimos movimientos que realizo la cuenta.
//Clase SaldoCuentas_---------------------------------------------------------------------------
// Clase SaldoCuentas que representa la ventana de visualización de saldo y historial de transacciones
public class SaldoCuentas extends javax.swing.JFrame {
    // Fondo de la ventana
    public Fondo imagen = new Fondo(); 
    
    // Modelo de tabla por defecto para la visualización del historial de transacciones
    DefaultTableModel dt = new DefaultTableModel();
    
    // Selector de idiomas
    JComboBox<String> idiomas;
  
    // Variables para almacenar el número de cuenta y la tarjeta asociada
    static String  cuentat;
    static String  tarjeta;
    
    // Variable para almacenar el saldo actual de la cuenta
    double dato;
    
    // Constructor de la clase
    public SaldoCuentas(String cuentat, String tarjeta) {   
        this.cuentat = cuentat;
        this.tarjeta = tarjeta;
        
        // Instancia de la clase funcionalidad para realizar operaciones relacionadas con las cuentas
        funcionalidad fun = new funcionalidad();
        
        // Lectura del saldo actual de la cuenta desde el archivo correspondiente
        dato = (double)fun.leerSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuentat+".txt");
        
        // Identificación de la moneda de la cuenta
        String monedaCuenta = processFile("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuentat+".txt");
        
        // Instancia de la clase historial para manejar el historial de transacciones de la cuenta
        historial his = new historial(cuentat,tarjeta);
        
        // Búsqueda de transacciones relacionadas con la cuenta en el archivo de registro
        String dattt = his.findMatchingLines("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\registro\\registros.txt",cuentat);
        
        // Configuración del fondo de la ventana y sus componentes
        this.setContentPane(imagen);
        initComponents();
        transpC(cuentat,dato,dattt,monedaCuenta);
        
        // Definición de nombres de columnas para la tabla de historial
        String []  nombres = new String []{"Fecha","Hora","TipoTransaccion","Saldo","Cuenta"};
        dt.setColumnIdentifiers(nombres);
   
        // La ventana no se puede redimensionar
        setResizable(false);
        
        // Configuración de los botones
        atras.setIcon(setIcono("/imagenes/atras.png",atras));
        atras.setPressedIcon(setIconoPrecionado("/imagenes/atras.png",atras,30,30));
        act.setIcon(setIcono("/imagenes/act.png",act));
        act.setPressedIcon(setIconoPrecionado("/imagenes/act.png",act,30,30));
    }
    
    // Método para procesar el contenido del archivo y reconocer la moneda de la cuenta
    public static String processFile(String filePath) {
        StringBuilder result = new StringBuilder();

        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                String message = recognizeCurrency(line);
                if (!message.isEmpty()) {
                    if (result.length() > 0) {
                        result.append("\n"); // Añadir un salto de línea entre mensajes
                    }
                    result.append(message);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        return result.toString();
    }

    // Método para reconocer la moneda de la cuenta a partir de una línea del archivo
    public static String recognizeCurrency(String line) {
        if (line.contains("eu:")) {
            return "SU CUENTA ESTA EN EUROS";
        } else if (line.contains("dlr:")) {
            return "SU CUENTA ESTA EN DOLARES";
        } else if (line.contains("bs:")) {
            return "SU CUENTA ESTA EN BOLIVIANOS";
        } else {
            return "";
        }
    }
    
    // Método para cambiar los textos de los componentes según el idioma seleccionado
    public void cambiarTextos() {
        if ("Русский".equals((String) idiomas.getSelectedItem())) {
            // Cambiar los textos de los componentes al ruso
            texto1.setText("ДОБРО ПОЖАЛОВАТЬ");
            texto2.setText("БАНАНИТА НАЦИОНАЛЬНЫЙ БАНК");
            texto3.setText("(Внимание 24 часа в сутки)");
        } else {
            if ("English".equals((String) idiomas.getSelectedItem())) {
                // Cambiar los textos de los componentes al inglés
                texto1.setText("WELCOME");
                texto2.setText("BANANITA NATIONAL BANK");
                texto3.setText("(Attention 24 hours a day)");
            } else {
                if ("Español".equals((String) idiomas.getSelectedItem())) {
                    // Cambiar los textos de los componentes al español
                    texto1.setText("BIENVENIDOS");
                    texto2.setText("BANCO NACIONAL BANANITA");
                    texto3.setText("(Atención las 24 hrs del día)");
                }
            }
        }
    }

    // Método para convertir un texto en formato HTML
    public String StrToHtml(String texto) {
        return "<html>" + texto.replace("\n", "<br>") + "</html>";
    }

    // Método para configurar los valores de los componentes de la ventana
    public void transpC(String nom, double dato,String textos, String datomoneda){
        String datos = String.valueOf(dato);
        cuenta.setText(nom);
        cuenta.setContentAreaFilled(false);
        cuenta.setBorderPainted(false);
        saldo.setText(datos);
        saldo.setContentAreaFilled(false);
        saldo.setBorderPainted(false);
        labeltxt.setText(StrToHtml(textos)+"\n");
        saldo1.setText(datomoneda);
        saldo1.setContentAreaFilled(false);
        saldo1.setBorderPainted(false);
//simplemente se le ingresa el texto necesario a los diferentes elemntos de la clase grafica
    }
}
//----------------------------------------------------------------------------------------

*Clase contra:

En esta clase se modificara el pin de la tarjeta en modo grafico.

Lo que se necesita es el pin antiguo y repetir el nuevo pin 2 veces para verificar hacemos esto llamando a otra clase llamada "funcion" que ahi se encuentra la logica detras de esto.
Reglas: el nuevo pin solo debe tener 3 caracteres y solo contener numeros.

Solo se comentara lo necesario ya que lo demas es parte del IDE: // Método invocado cuando se realiza una acción en el campo de contraseña actual
private void contraActualActionPerformed(java.awt.event.ActionEvent evt) {                                             
    // Se deja vacío ya que no hay código específico que se deba ejecutar aquí
}                                            

// Método invocado cuando se realiza una acción en el campo de contraseña nueva
private void contraNuevaActionPerformed(java.awt.event.ActionEvent evt) {                                            
    // Se deja vacío ya que no hay código específico que se deba ejecutar aquí
}                                           

// Método invocado cuando se realiza una acción en el campo de confirmación de contraseña nueva
private void contraNueva1ActionPerformed(java.awt.event.ActionEvent evt) {                                             
    // Se deja vacío ya que no hay código específico que se deba ejecutar aquí
}                                            

// Método invocado cuando se realiza una acción en el botón de confirmación de cambio de contraseña
private void confirmarActionPerformed(java.awt.event.ActionEvent evt) {                                          
    // Se intenta realizar el cambio de contraseña y se muestra un mensaje de éxito o error según el resultado
    boolean cop = CambiodeContra();
    if(cop){
        try {
            reemplazarPinEnArchivo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjeta + ".txt", pinnew);
        } catch (IOException e) {
            e.printStackTrace();
        }
        JOptionPane.showMessageDialog(null, "CAMBIO DE PIN REALIZADO CON EXITO");
        menu pel = new menu(tarjeta, cuenta);
        pel.setVisible(true);
        dispose();
    } else {
        JOptionPane.showMessageDialog(null, "ERROR AL INGRESAR NUEVO PIN"+"\n"+"POSIBLES ERRORES:"+
        "\n"+"*EL PIN ANTIGUO NO COINCIDE"+
        "\n"+"*NO COINCIDEN LOS NUEVO PIN"+
        "\n"+"*INTENTA INGRESAR LETRAS, SOLO SE PERMITEN NUMEROS"+
        "\n"+"*EL NUEVO PIN TIENE MAS DE 3 CARACTERES");
    }
}                                         

// Método invocado cuando se realiza una acción en el selector de idiomas
private void idiomasActionPerformed(java.awt.event.ActionEvent evt) {                                        
    // Este método se deja vacío ya que no hay código específico que se deba ejecutar aquí
}                                       

// Método para verificar si una cadena contiene solo números
public boolean esSoloNumeros(String texto) {
    return texto != null && !texto.isEmpty() && texto.matches("[0-9]+");
}

// Método para reemplazar el PIN almacenado en un archivo por uno nuevo
public static void reemplazarPinEnArchivo(String archivoRuta, String nuevoPin) throws IOException {
    // Se crea un archivo temporal para realizar el reemplazo del PIN
    File archivoOriginal = new File(archivoRuta);
    File archivoTemporal = new File(archivoRuta + ".tmp");

    try (BufferedReader reader = new BufferedReader(new FileReader(archivoOriginal));
        BufferedWriter writer = new BufferedWriter(new FileWriter(archivoTemporal))) {

        String linea;
        while ((linea = reader.readLine()) != null) {
            // Se reemplaza la línea que contiene el PIN con el nuevo PIN
            if (linea.startsWith("pin: ")) {
                linea = "pin: " + nuevoPin;
            }
            writer.write(linea);
            writer.newLine();
        }
    }

    // Se elimina el archivo original y se renombra el archivo temporal
    if (!archivoOriginal.delete()) {
        System.out.println("No se pudo eliminar el archivo original");
        return;
    }
    if (!archivoTemporal.renameTo(archivoOriginal)) {
        System.out.println("No se pudo renombrar el archivo temporal");
    }
}

// Método para realizar el cambio de contraseña
private boolean CambiodeContra(){
    // Se lee el PIN antiguo almacenado en el archivo correspondiente a la tarjeta
    int pinant = fun.leerPin("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjeta + ".txt");
    String pinants = contraActual.getText();
    pinnew = contraNueva1.getText();
    String pinnewConf = contraNueva.getText();
    int pintantcomp = Integer.parseInt(pinants);
    
    // Se verifican las condiciones para realizar el cambio de contraseña
    if(pinant == pintantcomp){
        if(pinnew.equals(pinnewConf)){
            if(esSoloNumeros(pinnew)){
                return true; // Se permite el cambio de PIN
            } else {
                return false; // El nuevo PIN no contiene solo números
            }
        } else {
            return false; // Los nuevos PIN no coinciden
        }
    } else {
        return false; // El PIN antiguo es incorrecto
    }
}

//------------------------------------------------------------------------------------------
*Clase funcionalidad
Esta clase lo unico que tiene son funciones que seran llamadas por otras clases para poder usar las funciones de esta clase ya sea obetner el pin, leer el saldo de la cuenta, etc:

import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;

/**
 * Esta clase proporciona funcionalidades comunes para el sistema del cajero automático.
 */
public class funcionalidad {
    
    // Método para leer el PIN desde un archivo de texto
    public  int leerPin(String nombreArchivo) {
         int pin = 0;
        try {
            // Abre el archivo
            File archivo = new File(nombreArchivo);
            Scanner scanner = new Scanner(archivo);

            // Busca la línea que contiene "pin:" y guarda lo que sigue
            while (scanner.hasNextLine()) {
                String linea = scanner.nextLine();
                if (linea.contains("pin:")) {
                    String pinStr = linea.substring(linea.indexOf("pin:") + 4).trim();
                    pin = Integer.parseInt(pinStr);
                    break; // Termina el bucle al encontrar la línea con "pin:"
                }
            }

            // Cierra el scanner
            scanner.close();
        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("El PIN no es un número válido: " + e.getMessage());
        }
        return pin;
    }
    
    // Método para leer el saldo desde un archivo de texto
    public  double leerSaldo(String nombreArchivo) {
        double saldo = 0;
        try {
            File archivo = new File(nombreArchivo);
            Scanner scanner = new Scanner(archivo);

            while (scanner.hasNextLine()) {
                String linea = scanner.nextLine();
                if (linea.contains("bs:") || linea.contains("eu:") || linea.contains("dlr:")) {
                    // Ajustamos la expresión regular para permitir decimales
                    String saldoString = linea.replaceAll("[^0-9.-]", "");
                    int puntoIndex = saldoString.indexOf('.');
                    if (puntoIndex != -1) {
                        saldoString = saldoString.substring(0, puntoIndex + 3); // Tomamos dos decimales después del punto
                    }
                    double saldoNumerico = Double.parseDouble(saldoString);
                    saldo += saldoNumerico;
                }
            }

            scanner.close();
        } catch (FileNotFoundException e) {
            System.err.println("Archivo no encontrado: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("El saldo no es un número válido: " + e.getMessage());
        }
        return saldo;
    }

    // Método para verificar si un archivo existe en una ruta dada
    public static boolean verificarExistencia(String nombreArchivo) {
        File archivo = new File(nombreArchivo);
        return archivo.exists(); // Devuelve true si el archivo existe, false si no existe
    }
   
    // Método para leer el contenido de un archivo de texto
    public static String leer(String rutaArchivo) {
        StringBuilder contenido = new StringBuilder();

        try {
            BufferedReader br = new BufferedReader(new FileReader(rutaArchivo));
            String linea;

            // Leer el contenido del archivo línea por línea
            while ((linea = br.readLine()) != null) {
                // Verifica si la línea contiene "nombre:" o "pin:"
                if (!linea.contains("nombre:") && !linea.contains("pin:")) {
                    contenido.append(linea).append("\n"); // Agregar la línea al contenido con un salto de línea
                }
            }
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

        return contenido.toString();
    }
    
    // Método para obtener el nombre almacenado en un archivo de texto
    public static String obtenerNombre(String rutaArchivo) {
        String nombre = null;

        try {
            BufferedReader br = new BufferedReader(new FileReader(rutaArchivo));
            String linea;

            // Leer el contenido del archivo línea por línea
            while ((linea = br.readLine()) != null) {
                // Verifica si la línea contiene "nombre:"
                if (linea.contains("nombre:")) {
                    // Encuentra la posición de "nombre: " en la línea
                    int indiceNombre = linea.indexOf("nombre: ");
                    // Extrae el texto después de "nombre: "
                    nombre = linea.substring(indiceNombre + "nombre: ".length());
                    // Rompe el bucle después de encontrar el nombre
                    break;
                }
            }
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

        return nombre;
    }
}
//----------------------------------------------------------------------------------------------------

*Clase historial:

Esta clase se encarga de guardar los movimientos que se hace dentro de la cuenta en formato: "Cuenta pasada por parametro"+"fecha""Hora""minutos"+"accion":

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Stack;

/**
 * Esta clase gestiona el historial de transacciones de una cuenta en el cajero automático.
 * Permite buscar y agregar registros, así como obtener la fecha y hora actuales.
 */
public class historial {
    
    // Atributos de la clase
    String cuenta; // Número de cuenta asociado al historial
    String Accion; // Acción realizada en la cuenta (por ejemplo, retiro, depósito, etc.)
    
    /**
     * Constructor de la clase `historial`.
     * @param cuenta Número de cuenta asociado al historial.
     * @param Accion Acción realizada en la cuenta.
     */
    public historial(String cuenta, String Accion){
        this.cuenta = cuenta;
        this.Accion = Accion;
    }
    
    // Ruta del archivo de registro
    String dir = "C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\registro\\registros.txt";
    
    /**
     * Método estático para encontrar líneas que coincidan con un prefijo en un archivo.
     * @param filePath Ruta del archivo.
     * @param prefix Prefijo que se busca.
     * @return Una cadena que contiene las líneas coincidentes.
     */
    public static String findMatchingLines(String filePath, String prefix) {
        Stack<String> stack = new Stack<>();
        StringBuilder result = new StringBuilder();
        int count = 0;
        String prefixWithColon = prefix + ": ";

        // Lee el archivo y guarda las líneas en un stack
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                stack.push(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Lee desde el stack (líneas de abajo hacia arriba) buscando coincidencias con el prefijo
        while (!stack.isEmpty() && count < 10) {
            String line = stack.pop();
            if (line.startsWith(prefixWithColon)) {
                // Guarda la línea que coincide con el prefijo
                result.append(line).append("\n");
                count++;
            }
        }

        return result.toString();
    }
    
    /**
     * Método estático para obtener la fecha actual.
     * @return Objeto `LocalDate` que representa la fecha actual.
     */
    public static LocalDate obtenerFechaActual() {
        return LocalDate.now();
    }
    
    /**
     * Método estático para obtener la hora actual con segundos como enteros.
     * @return Cadena que representa la hora actual con segundos como enteros.
     */
    public static String getCurrentTimeWithIntegerSeconds() {
        // Obtiene la hora actual
        LocalDateTime now = LocalDateTime.now();
        
        // Formatea la hora actual a una cadena, incluyendo segundos como enteros
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("HH:mm:ss");
        return now.format(formatter);
    }
    
    /**
     * Método estático para agregar una línea a un archivo.
     * @param filePath Ruta del archivo.
     * @param nuevaLinea Línea a agregar.
     */
    public static void agregarLinea(String filePath, String nuevaLinea) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath, true))) {
            writer.write(nuevaLinea);
            writer.newLine();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    /**
     * Método para guardar una nueva entrada en el historial.
     * Obtiene la fecha y hora actuales, y guarda la acción realizada en la cuenta en el archivo de historial.
     */
    public void guardar(){
        // Obtiene la fecha actual
        LocalDate fechaActual = LocalDate.now();
        // Convierte la fecha actual a String
        String fechaString = fechaActual.toString();
        
        // Obtiene la hora actual
        String currentTime = getCurrentTimeWithIntegerSeconds();
        
        // Crea la cadena que representa el registro
        String hist = cuenta + ": " + fechaString + " " + currentTime + " " + Accion + "";
        
        // Agrega la cadena al archivo de historial
        agregarLinea(dir, hist);
    }
}
//FIN_---------------------------------------------------------------------------------------------

*Clase historialTransacciones:

Esta clase existe especialmente para las transacciones entre cuentas ya que no valdria la pena clase "historial", la funcionalidad es basicamente mandar las cuentas que son manipuladas por parametro guardando 2 registros dentro de archivo de registros 1 siendo el que recibe el dinero y el otro que transfiere el dinero:
 //----------------------------------------------------------------------------------------------
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Stack;

/**
 * Esta clase gestiona el historial de transacciones entre cuentas del cajero automático.
 * Permite buscar y agregar registros de transacciones, incluyendo depósitos e ingresos.
 */
public class historialTransacciones {
    
    // Atributos de la clase
    String cuenta1; // Número de cuenta de origen
    String cuenta2; // Número de cuenta de destino
    double deposito; // Monto depositado
    
    // Ruta del archivo de registro
    String dir = "C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\registro\\registros.txt";
    
    /**
     * Constructor de la clase `historialTransacciones`.
     * @param cuenta1 Número de cuenta de origen.
     * @param cuenta2 Número de cuenta de destino.
     * @param deposito Monto depositado.
     */
    public historialTransacciones(String cuenta1, String cuenta2, double deposito){
        this.cuenta1 = cuenta1;
        this.cuenta2 = cuenta2;
        this.deposito = deposito;
    }
    
    /**
     * Método estático para encontrar líneas que coincidan con un prefijo en un archivo.
     * @param filePath Ruta del archivo.
     * @param prefix Prefijo que se busca.
     * @return Una cadena que contiene las líneas coincidentes.
     */
    public static String findMatchingLines(String filePath, String prefix) {
        Stack<String> stack = new Stack<>();
        StringBuilder result = new StringBuilder();
        int count = 0;
        String prefixWithColon = prefix + ": ";

        // Lee el archivo y guarda las líneas en un stack
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                stack.push(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Lee desde el stack (líneas de abajo hacia arriba) buscando coincidencias con el prefijo
        while (!stack.isEmpty() && count < 10) {
            String line = stack.pop();
            if (line.startsWith(prefixWithColon)) {
                // Guarda la línea que coincide con el prefijo
                result.append(line).append("\n");
                count++;
            }
        }

        return result.toString();
    }
    
    /**
     * Método estático para obtener la fecha actual.
     * @return Objeto `LocalDate` que representa la fecha actual.
     */
    public static LocalDate obtenerFechaActual() {
        return LocalDate.now();
    }
    
    /**
     * Método estático para obtener la hora actual con segundos como enteros.
     * @return Cadena que representa la hora actual con segundos como enteros.
     */
    public static String getCurrentTimeWithIntegerSeconds() {
        // Obtiene la hora actual
        LocalDateTime now = LocalDateTime.now();
        
        // Formatea la hora actual a una cadena, incluyendo segundos como enteros
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("HH:mm:ss");
        return now.format(formatter);
    }
    
    /**
     * Método estático para agregar una línea a un archivo.
     * @param filePath Ruta del archivo.
     * @param nuevaLinea Línea a agregar.
     */
    public static void agregarLinea(String filePath, String nuevaLinea) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath, true))) {
            writer.write(nuevaLinea);
            writer.newLine();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    /**
     * Método para guardar una transacción de depósito en el historial.
     * Guarda la fecha, hora, cuenta de origen y monto depositado en el archivo de historial.
     */
    public void guardarDeposito(){
        // Obtiene la fecha actual
        LocalDate fechaActual = LocalDate.now();
        // Convierte la fecha actual a String
        String fechaString = fechaActual.toString();
        
        // Obtiene la hora actual
        String currentTime = getCurrentTimeWithIntegerSeconds();
        
        // Crea la cadena que representa el registro de depósito
        String hist = cuenta1 + ": " + fechaString + " " + currentTime + " " + "SE DEPOSITO: " + deposito + " A LA CUENTA: " + cuenta2;
        
        // Agrega la cadena al archivo de historial
        agregarLinea(dir, hist);
    }
    
    /**
     * Método para guardar una transacción de ingreso en el historial.
     * Guarda la fecha,
//---------------------------------------------------------------------------------------------

*Clase inicio:

Esta clase grafica es la primera que aparece al momento de correr el programa que lo que hace es verificar la existencia de tu tarjerta de credito y pin si todo es correcto te manda a los botones.

package cajero;

import java.awt.Graphics;
import java.awt.Image;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

// Se importan las clases necesarias para la interfaz gráfica y el manejo de eventos

public class inicio extends javax.swing.JFrame {
    // Declaración de variables de clase
    String tarjetaText;
    String pinText;
    int pin;

    // Constructor de la clase inicio
    public inicio() {
        // Se establece un fondo para la ventana de inicio
        this.setContentPane(imagen);
        // Se inicializan los componentes de la interfaz gráfica
        initComponents();  
        // Se deshabilita la capacidad de redimensionar la ventana
        setResizable(false);
        // Se configuran las imágenes de los botones
        sig.setIcon(setIcono("/imagenes/sig.png",sig));
        sig.setPressedIcon(setIconoPrecionado("/imagenes/sig.png",sig,30,30));
    }
    
    // Creación de una instancia de la clase funcionalidad para utilizar sus métodos
    funcionalidad fun = new funcionalidad();

    // Método generado automáticamente para inicializar los componentes de la interfaz
    private void initComponents() {
        // Se crean los componentes de la interfaz gráfica y se definen sus propiedades
        // (etiquetas de texto, botones, campos de texto, etc.)
    }

    // Método para manejar el evento de hacer clic en el botón "sig"
    private void sigActionPerformed(java.awt.event.ActionEvent evt) {                                    
        // Se obtiene el número de tarjeta y el PIN ingresados por el usuario
        tarjetaText = numCuenta.getText();
        int tarjeta = Integer.parseInt(tarjetaText);
        pinText =  contra.getText();
        pin = Integer.parseInt(pinText);
        
        // Se verifica si las credenciales son correctas llamando al método verificarCredenciales
        if (verificarCredenciales()) {
            // Si las credenciales son correctas, se abre la siguiente ventana y se cierra la actual
            CuentasBotones v = new CuentasBotones( tarjetaText);
            numCuenta.setText("");
            numCuenta.requestFocus();
            v.setVisible(true);
            dispose(); 
        } else {
            // Si las credenciales no son correctas, se muestra un mensaje de error
            JOptionPane.showMessageDialog(null, "ERROR AL INGRESAR PIN O TARJETA NO EXISTE");
        }
    }    

    // Método para manejar el evento de cambiar el idioma seleccionado en el JComboBox "idiomas"
    private void idiomasActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // Se llama al método cambiarTextos() para actualizar los textos de la interfaz
        cambiarTextos();
    }                                       

    // Método para verificar si las credenciales ingresadas son correctas
    private boolean verificarCredenciales() {
        // Se verifica si la tarjeta existe y si el PIN ingresado coincide
        boolean existe = fun.verificarExistencia("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjetaText + ".txt");
        boolean existeCont = pin==(fun.leerPin("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjetaText + ".txt"));
        
        // Se imprime en consola si existe la tarjeta y si el PIN coincide
        System.out.println("Existe usuario: " + existe);
        System.out.println("Coincide contraseña: " + existeCont);
        
        // Se devuelve true si la tarjeta existe y el PIN coincide; de lo contrario, se devuelve false
        return (existe && existeCont);
    }
}
//Solo se comento la parte que es funcional dentro de la clase ya que lo demas es propio del IDE-------------------------------------------------------------------------------------------


*Clase menu:

Esta clase es la mas importante porque desde esta apartado grafico se puede acceder a las diferentes clases.
// Importaciones necesarias para la funcionalidad gráfica
import java.awt.Graphics; // Para dibujar gráficos en componentes
import java.awt.Image; // Para representar imágenes
import javax.swing.Icon; // Interfaz para representar iconos
import javax.swing.ImageIcon; // Para manejar imágenes en forma de iconos
import javax.swing.JButton; // Componente botón
import javax.swing.JComboBox; // Componente ComboBox
import javax.swing.JPanel; // Panel contenedor para organizar componentes

// Clase que representa el menú principal
public class menu extends javax.swing.JFrame {
    // Componentes de la interfaz gráfica
    private JComboBox<String> idiomasComboBox; // ComboBox para seleccionar el idioma
    static String tarjeta; // Número de tarjeta
    static String cuenta; // Número de cuenta
    public Fondo imagen = new Fondo(); // Fondo de la ventana

    // Constructor de la clase
    public menu(String tarjeta,String cuenta) {
        // Creación de una instancia de funcionalidad
        funcionalidad ddd = new funcionalidad();
        // Obtener el nombre del titular de la tarjeta
        String nomn = ddd.obtenerNombre("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\tarjetas\\" + tarjeta + ".txt"); 

        // Establecer el fondo de la ventana
        this.setContentPane(imagen);
        // Inicializar los componentes de la interfaz gráfica
        initComponents();
        // Configurar los textos y transparencias
        transp(nomn,cuenta);
        // Asignar los valores de tarjeta y cuenta
        this.tarjeta=tarjeta;
        this.cuenta=cuenta;
        // No permitir redimensionamiento de la ventana
        setResizable(false);

        // Crear un panel
        JPanel panel = new JPanel();
        panel.setLayout(null); // Diseño sin diseño automático

        // Configurar los iconos de los botones
        // [Omisión de detalles de configuración para brevedad]

        // Configuración de los eventos de los botones
    }

    // Método para cambiar los textos de la interfaz según el idioma seleccionado
    public void cambiarTextos() {
        String leng = (String) idiomasComboBox.getSelectedItem();

        if ("Русский".equals(leng)) {
            // Cambiar los textos a ruso
            texto1.setText("Имя:");
            texto2.setText("Выберите тип транзакции, который вы хотите");
        } else if ("English".equals(leng)) {
            // Cambiar los textos a inglés
            texto1.setText("Name:");
            texto2.setText("Choose the type of Transaction you want");
        } else if ("Español".equals(leng)) {
            // Cambiar los textos a español
            texto1.setText("Nombre");
            texto2.setText("Elige el tipo de Transaccion Que quieras");
        }
    }

    // Método generado automáticamente para inicializar los componentes de la interfaz
    private void initComponents() {
        // Inicialización de los componentes gráficos y configuración de sus propiedades
    }

    // Eventos de los botones
    private void retirarActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // Acción al presionar el botón "retirar"
    }

// Evento al presionar el botón "depositar"
private void depositarActionPerformed(java.awt.event.ActionEvent evt) {                                          
    // Crear una instancia de la ventana para depositar
    OtroMontoI v = new OtroMontoI(cuenta, tarjeta);
    // Mostrar la ventana
    v.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

// Evento al presionar el botón "transferir"
private void transferirActionPerformed(java.awt.event.ActionEvent evt) {                                           
    // Crear una instancia de la ventana para transferir
    OtraCuenta v = new OtraCuenta(cuenta, tarjeta);
    // Mostrar la ventana
    v.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

// Evento al presionar el botón "contra"
private void contraActionPerformed(java.awt.event.ActionEvent evt) {                                       
    // Crear una instancia de la ventana para cambiar la contraseña
    contra v = new contra(tarjeta, cuenta);
    // Mostrar la ventana
    v.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

// Evento al presionar el botón "atras"
private void atrasActionPerformed(java.awt.event.ActionEvent evt) {                                      
    // Crear una instancia de la ventana de las cuentas
    CuentasBotones v = new CuentasBotones(tarjeta);
    // Mostrar la ventana
    v.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

// Evento al presionar el botón "saldo"
private void saldoActionPerformed(java.awt.event.ActionEvent evt) {                                      
    // Crear una instancia de la ventana para ver el saldo
    SaldoCuentas s = new SaldoCuentas(cuenta, tarjeta);
    // Mostrar la ventana
    s.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

// Evento al presionar el botón "cambio"
private void cambioActionPerformed(java.awt.event.ActionEvent evt) {                                       
    // Crear una instancia de la ventana para cambio de moneda
    CambioMoneda v = new CambioMoneda(cuenta, tarjeta);
    // Mostrar la ventana
    v.setVisible(true);
    // Cerrar la ventana actual
    dispose();
}

    // Método para configurar los textos y transparencias de la interfaz
    public void transp(String nom,String cuenta){
        // Configurar el texto del botón con el nombre
        BTNnombre.setText(nom);
        // Configurar el texto de la cuenta
        numCuentaLBL.setText(cuenta);
        // Configurar la apariencia de los botones
        BTNnombre.setContentAreaFilled(false);
        BTNnombre.setBorderPainted(false);
    }
}
//------------------------------------------------------------------------------------------

*Clase retiros:

En esta clase se mostraran las diferentes cantidades predeterminadas para retirar dinero y otro boton llamado "otro monto" para poder retirar el monto que se requiera
el unico "fallo" seria que no se tenga el suficiente saldo:

/*
 * Paquete que contiene la clase retiros.
 */
package cajero;

import java.awt.Graphics;
import java.awt.Image;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JPanel;

/**
 *
 * @author andres
 */
public class retiros extends javax.swing.JFrame {
    // Variables estáticas para la cuenta y la tarjeta
    static String cuenta;
    static String tarjeta;
    // Fondo de la ventana
    public Fondo imagen = new Fondo();  

    /**
     * Constructor de la clase.
     * @param cuenta El número de cuenta del usuario.
     * @param tarjeta El número de tarjeta del usuario.
     */
    public retiros(String cuenta, String tarjeta) {
        // Inicialización de las variables
        this.cuenta=cuenta;
        this.tarjeta=tarjeta;
        // Establecer el fondo de la ventana
        this.setContentPane(imagen);
        // Inicializar componentes de la ventana
        initComponents();
        // Hacer que la ventana no sea redimensionable
        setResizable(false);
        // Configurar botones con imágenes y eventos
        configurarBotones();
    }
    
    CambiosEnSaldo cambio = new CambiosEnSaldo();

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        texto2 = new javax.swing.JLabel();
        texto1 = new javax.swing.JLabel();
        BTNCINCUENTA = new javax.swing.JButton();
        BTNSETENTA = new javax.swing.JButton();
        BTNCIEN = new javax.swing.JButton();
        BTNCIENTOCINCUENTA = new javax.swing.JButton();
        BTNDOSIENTOS = new javax.swing.JButton();
        atras = new javax.swing.JButton();
        BTONDiez = new javax.swing.JButton();
        saldo7 = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        // Configuración de fuentes y colores
        texto2.setFont(new java.awt.Font("Arial Black", 3, 36)); 
        texto2.setForeground(new java.awt.Color(0, 51, 102));
        texto2.setText("Elige el tipo  el monto  que quiera Retirar");

        texto1.setBackground(new java.awt.Color(51, 51, 51));
        texto1.setFont(new java.awt.Font("Arial Black", 3, 48)); 
        texto1.setText("BNB");

        // Configuración de botones (se omite el código por brevedad)

        // Configuración de eventos para botones (se omite el código por brevedad)

        // Ajustes de diseño de la ventana (se omite el código por brevedad)

        pack();
    }// </editor-fold>                        

    // Método para el evento al presionar el botón "atras"
    private void atrasActionPerformed(java.awt.event.ActionEvent evt) {                                      
        // Crear una instancia de la ventana de menú
        menu v = new menu(tarjeta, cuenta);
        // Mostrar la ventana
        v.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }                                     

    // Método para el evento al presionar el botón "saldo7"
    private void saldo7ActionPerformed(java.awt.event.ActionEvent evt) {                                       
        // Crear una instancia de la ventana para otro monto
        OtroMonto v = new OtroMonto(cuenta, tarjeta);
        // Mostrar la ventana
        v.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }                                      

    // Método para el evento al presionar el botón "BTONDiez"
    private void BTONDiezActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // Realizar el decremento del saldo por 10
        cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",10.0,cuenta);
        // Crear una instancia de la ventana de menú
        menu i = new menu(tarjeta,cuenta);
        // Mostrar la ventana
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose(); 
    }                                        

    // Método para el evento al presionar el botón "BTNCINCUENTA"
    private void BTNCINCUENTAActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // Realizar el decremento del saldo por 50
        cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",50.0,cuenta);
        // Crear una instancia de la ventana de menú
        menu i = new menu(tarjeta,cuenta);
        // Mostrar la ventana
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose(); 
    }                                            

    // Método para el evento al presionar el botón "BTNDOSIENTOS"
    private void BTNDOSIENTOSActionPerformed(java.awt.event.ActionEvent evt) {                                             
        // Realizar el decremento del saldo por 200
        cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",200.0,cuenta);
        // Crear una instancia de la ventana de menú
        menu i = new menu(tarjeta,cuenta);
        // Mostrar la ventana
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }                                            

    // Método para el evento al presionar el botón "BTNSETENTA"
    private void BTNSETENTAActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // Realizar el decremento del saldo por 70
        cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",70.0,cuenta);
        // Crear una instancia de la ventana de menú
        menu i = new menu(tarjeta,cuenta);
        // Mostrar la ventana
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }                                          
// Método para el evento al presionar el botón "BTNCIENTOCINCUENTA"
    private void BTNCIENTOCINCUENTAActionPerformed(java.awt.event.ActionEvent evt) {                                                   
        // Realizar el decremento del saldo por 150
        cambio.DecrementoSaldo("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt",150.0,cuenta);
        // Crear una instancia de la ventana de menú
        menu i = new menu(tarjeta,cuenta);
        // Mostrar la ventana
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose(); 
    }
//Lo que sigue es propio del iDE sin necesidad de explicacion--------------------------------------

*Clase transaccionIII:

Esta clase es importante poque se encarga de hacer las transferencias de dinero entre las cuentas conteniendo botones con valores predeterminados y otro monto que se ingresa el monto que desea transferir:

package cajero;

import java.awt.Graphics;
import java.awt.Image;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JPanel;

/**
 * La clase `transaccionIII` representa la ventana de la interfaz de usuario
 * para la transacción de transferencia entre cuentas.
 * Esta ventana permite al usuario seleccionar el monto a transferir.
 * 
 * @author andres
 */
public class transaccionIII extends javax.swing.JFrame {
     // Declaración de variables estáticas para almacenar los números de cuenta y tarjeta
     static String cuenta;
     static String tarjeta;
     static String cuenta2;
     // Instancia de la clase Fondo para establecer un fondo personalizado en la interfaz
    public Fondo imagen = new Fondo();  
    
    /**
     * Constructor de la clase `transaccionIII`.
     * 
     * @param cuenta Número de cuenta del remitente.
     * @param tarjeta Número de tarjeta del remitente.
     * @param cuenta2 Número de cuenta del destinatario.
     */
    public transaccionIII(String cuenta,String tarjeta,String cuenta2) {
        // Asignación de valores a las variables de cuenta, tarjeta y cuenta2
        this.cuenta=cuenta;
        this.tarjeta=tarjeta;
        this.cuenta2=cuenta2;
        // Establecimiento del fondo de la ventana de la interfaz
        this.setContentPane(imagen);
        // Inicialización de los componentes de la interfaz
        initComponents();
        // Se establece que la ventana no sea redimensionable
        setResizable(false);
              
        // Configuración de la apariencia de los botones de la interfaz
        saldo7.setIcon(setIcono("/imagenes/otroMonto.png",saldo7));
        saldo7.setPressedIcon(setIconoPrecionado("/imagenes/otroMonto.png",saldo7,30,30));
        
        // Configuración del botón "atras"
        atras.setIcon(setIcono("/imagenes/atras.png",atras));
        atras.setPressedIcon(setIconoPrecionado("/imagenes/atras.png",atras,30,30));    
    }
    
    // Instancia de la clase CambiosEnSaldo para realizar las operaciones de transferencia
    CambiosEnSaldo cambio = new CambiosEnSaldo();

    /**
     * Método generado automáticamente por el editor visual para inicializar
     * los componentes de la interfaz gráfica.
     */
    @SuppressWarnings("unchecked")
    private void initComponents() {
        // Declaraciones de componentes de la interfaz
        texto2 = new javax.swing.JLabel();
        texto1 = new javax.swing.JLabel();
        BTNCINCUENTA = new javax.swing.JButton();
        BTNSETENTA = new javax.swing.JButton();
        BTNCIEN = new javax.swing.JButton();
        BTNCIENTOCINCUENTA = new javax.swing.JButton();
        BTNDOSIENTOS = new javax.swing.JButton();
        atras = new javax.swing.JButton();
        BTONDiez = new javax.swing.JButton();
        saldo7 = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        // Configuración de etiquetas de texto
        texto2.setFont(new java.awt.Font("Arial Black", 3, 36));
        texto2.setForeground(new java.awt.Color(0, 51, 102));
        texto2.setText("Elige el tipo  el monto  que quiera Transferir");

        texto1.setBackground(new java.awt.Color(51, 51, 51));
        texto1.setFont(new java.awt.Font("Arial Black", 3, 48));
        texto1.setText("BNB");

        // Configuración de botones con montos predefinidos
        BTNCINCUENTA.setFont(new java.awt.Font("Dialog", 1, 36));
        BTNCINCUENTA.setForeground(new java.awt.Color(0, 0, 0));
        BTNCINCUENTA.setText("50");
        BTNCINCUENTA.setBorderPainted(false);
        BTNCINCUENTA.setFocusPainted(false);
        BTNCINCUENTA.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                BTNCINCUENTAActionPerformed(evt);
            }
        });

        // Similar configuración para los demás botones...

        // Configuración del botón "atras"
        atras.setBorderPainted(false);
        atras.setContentAreaFilled(false);
        atras.setFocusPainted(false);
        atras.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                atrasActionPerformed(evt);
            }
        });

        // Similar configuración para los demás botones...

        // Organización de los componentes en la ventana
        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            // Configuración horizontal de los componentes...
        );
        layout.setVerticalGroup(
            // Configuración vertical de los componentes...
        );
        pack();
    }

    // Métodos para manejar eventos de los botones...

    // Método para manejar el evento del botón "atras"
    private void atrasActionPerformed(java.awt.event.ActionEvent evt) {
        // Creación de una nueva instancia del menú principal
        menu v = new menu(tarjeta,cuenta);
        // Hacer visible la ventana del menú principal
        v.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }

    // Método para manejar el evento del botón "saldo7"
    private void saldo7ActionPerformed(java.awt.event.ActionEvent evt) {
        // Creación de una nueva instancia para especificar un monto personalizado
        MontoTransacciones v = new MontoTransacciones(cuenta,tarjeta,cuenta2);
        // Hacer visible la ventana para especificar el monto
        v.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }

    // Métodos para manejar eventos de los botones de montos predefinidos...
}
    private void BTONDiezActionPerformed(java.awt.event.ActionEvent evt) {
        // Transferencia de 10 unidades monetarias entre cuentas
        cambio.transferirDinero("C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta+".txt","C:\\Users\\fband\\Downloads\\cajero (1)\\cajero\\cuentas\\"+cuenta2+".txt",10.0,cuenta,cuenta2);
        // Creación de una nueva instancia del menú principal
        menu i = new menu(tarjeta,cuenta);
        // Hacer visible la ventana del menú principal
        i.setVisible(true);
        // Cerrar la ventana actual
        dispose();
    }

    private void BTNCINCUENTAActionPerformed(java.awt.event.ActionEvent evt) {
        // Similar configuración para los demás botones...
    }

    private void BTNDOSIENTOSActionPerformed(java.awt.event.ActionEvent evt) {
        // Similar configuración para los demás botones...
    }

    private void BTNSETENTAActionPerformed(java.awt.event.ActionEvent evt) {
        // Similar configuración para los demás botones...
    }

    private void BTNCIENActionPerformed(java.awt.event.ActionEvent evt) {
        // Similar configuración para los demás botones...
    }

    private void BTNCIENTOCINCUENTAActionPerformed(java.awt.event.ActionEvent evt) {
        // Similar configuración para los demás botones...
    }

  //Lo demas es parte del propio IDE sin necesidad de explicacion porque no es modificable
}


