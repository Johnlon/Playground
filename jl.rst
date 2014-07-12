.. highlight:: scala

.. code:: scala

import java.io.FileInputStream
import org.pegdown.{Extensions, PegDownProcessor}
import scala.io.Source


this is a comment _underline_
**hello**

.. table:: Truth table for "not"

   =====  =====
     A    not A
   =====  =====
   False  True
   True   False
   =====  =====

.. code:: Example 2
    
    object Invert {
      def main(args: Array[String]) {
        val ScalaStart =  System.lineSeparator() + "`" + "``" + System.lineSeparator() + System.lineSeparator()
        val ScalaEnd =  System.lineSeparator() + "`" + "``" + System.lineSeparator()+ System.lineSeparator()
    
        val f = new FileInputStream(args(0))
    
        val body = Source.fromInputStream(f).getLines().map {
          l: String =>
            if (l.matches("^\\s*/\\*!\\s*")) {
              ScalaEnd
            } else if (l.matches("^\\s*\\*/\\s*")) {
              ScalaStart
            } else {
              l + System.lineSeparator()
            }
        }.mkString("")
    
        val md = ScalaStart + body + ScalaEnd
    
        println("MD:\n" + md)
        val pd = new PegDownProcessor(Extensions.ALL)
    
        val h: String = pd.markdownToHtml(md)
        println("\nHTML\n" + h)
      }
    }
