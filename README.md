# cx

import java.io.BufferedReader;
import java.io.DataInputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStreamReader;

import org.apache.log4j.BasicConfigurator;
import org.apache.log4j.Logger;
import org.apache.log4j.PropertyConfigurator;




public class LoggingSample {
	
 
private static Logger logger = Logger.getLogger(LoggingSample.class.getName());
public LoggingSample() {
	 BasicConfigurator.configure(); //configuring file
	  PropertyConfigurator.configure(getClass().getResource("D:\\SidhiVinayak\\3-12-2015\\log\\LogFileCreation\\src\\log4j.properties"));	//including log file
		
	}
public void check(){
	 try {
		 //Read File coding
		  FileInputStream fstream = new FileInputStream("D:\\textfile.txt");
		  DataInputStream in = new DataInputStream(fstream);
		  BufferedReader br = new BufferedReader(new InputStreamReader(in));
		  String strLine;
		 
			while((strLine = br.readLine()) != null) {
				  System.out.println(strLine);
			
		} 
		  in.close();
		}
	 catch(FileNotFoundException fe) {
		 logger.error("File not Found", fe);
		 logger.warn("This is a warning message");
		 logger.trace("This message will not be logged since log level is set as DEBUG");
	 }
	 catch (IOException e) {
			logger.error("IOException occured : ", e);
			//e.printStackTrace();
		}
}


 public static void main(String args[]){
	 LoggingSample obj = new LoggingSample();
	 obj.check();
	}
}

log4j.rootLogger=INFO, CONSOLE, R

log4j.appender.CONSOLE=org.apache.log4j.ConsoleAppender
log4j.appender.CONSOLE.layout=org.apache.log4j.PatternLayout
log4j.appender.CONSOLE.layout.ConversionPattern=[%t] %-5p %c %x - %m%n

log4j.appender.R=org.apache.log4j.RollingFileAppender
log4j.appender.R.layout=org.apache.log4j.PatternLayout
log4j.appender.R.layout.ConversionPattern=[%t] %-5p %c %x - %m%n
log4j.appender.R.File=${user.home}/logtest.log
log4j.appender.R.MaxFileSize=200KB
log4j.appender.R.MaxBackupIndex=2     
