package com.cts.memory;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;

public class App 
{
    @SuppressWarnings("resource")
	public static void main( String[] args ) throws IOException
    {
    	BufferedReader br = new BufferedReader(new FileReader("C:/Users/super/Downloads/Memory.txt"));
		 String line;
		 br.readLine();
		List<String> list=new ArrayList<String>();
		 while((line = br.readLine()) != null) {
			br.readLine();
		 	String[] columns = line.split(" ");		 	
		 	list.add(columns[18]);	
		 }
		 writeJsonSimpleDemo("abcd.json", list);
    }

	@SuppressWarnings({"unchecked" })
	private static void writeJsonSimpleDemo(String filename, List<String> list) throws IOException {
		// TODO Auto-generated method stub
		
		List<Double> array=new ArrayList<Double>();
		for(String s : list) {
			double res=Math.round(Double.parseDouble(s)*100)/1000;
			double fin=res/100;
			array.add(fin);
		}
		
		JSONObject result=new JSONObject();
		JSONArray values = new JSONArray();
		int n=1; 
		double sum=0;
    	for(Double str : array) {
    		
    			JSONObject sampleObject = new JSONObject();    			   		
    			sampleObject.put( n+"s", str);
    			values.add(sampleObject);
    			sum=sum+str;
    			n=n+1;
    	}
    	
    	double avg=sum/array.size();
    	double max=Collections.max(array);
    	
    	double roundOffMax = Math.round(max * 100.0) / 100.0;
    	double roundOffAvg = Math.round(avg * 100.0) / 100.0;
    	
    	result.put("AverageMemory(MB)", roundOffAvg);    	
    	result.put("values", values);
    	result.put("MaxMemory(MB)", roundOffMax);
    	result.put("Usecasename", "HomePage");
    	
    	System.out.println(result);
		
    	Files.write(Paths.get(filename),result.toJSONString().getBytes());
			
	}

}