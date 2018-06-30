# cybrilla

import java.util.*;
import java.math.Random;

class UrlShorten
{
    private HashMap<String,String> keyMap;
    private HashMap<String,String> valueMap;
    private Random rand;
    private int keylength;
    private String domain;
    UrlShorten()
    {
        keyMap=new HashMap<String,String>();
        valueMap=new HashMap<String,String>();
        rand=new Random();
        keyLength = 8;
		myChars = new char[62];
		for (int i = 0; i < 62; i++) {
			int j = 0;
			if (i < 10) {
				j = i + 48;
			} else if (i > 9 && i <= 35) {
				j = i + 55;
			} else {
				j = i + 61;
			}
			myChars[i] = (char) j;
    }
    domain="http://fkt.in"; 
    }
    URLShorten(int length, String newDomain) {
		this();
		this.keyLength = length;
		if (!newDomain.isEmpty()) {
			newDomain = sanitizeURL(newDomain);
			domain = newDomain;
		}
	}
     public string shortenUrl(String longURL)
    {
        String shortUrl="";
        if(validateURL(longURL))
        {
            longURL=sanitizeUrl(longURL);
        }
        if(valueMap.containsKey(longURL))
        shortUrl=domain+"/"+valueMap.get(longURL);
        else
        shortUrl=domain+"/"+getKey(longURL);
        return shortUrl;
    }
    public boolean validateURL(String longURL)
    {
        return true;
    }
    public String getKey(String longURL)
    {
     String key;
     key=generateKey();
     keyMap.put(key,longURL);
     valueMap.put(longURL,key);
     return key;
    }
    public String generateKey()
    {
        String key = "";
		boolean flag = true;
		while (flag) {
			key = "";
			for (int i = 0; i <= keyLength; i++) {
				key += myChars[myRand.nextInt(62)];
			}
			// System.out.println("Iteration: "+ counter + "Key: "+ key);
			if (!keyMap.containsKey(key)) {
				flag = false;
			}
		}
		return key;   
     }
    public string sanitizeUrl(String longURL1)
    {
        if(longURL1.subString(0,7).equals("http://"))
        longURL1=longURL1.subString(7);
        if(longURL1.subString(0,8).equals("http://"))
        longURL1=longURL1.subString(8);
        if(longURL1.indexOf(longURL1.length()-1)=='/')
        longURL1=longURL1.subString(0,longURL1.length()-1);
        return longURL1;
    }
}

public class Main
{
    public static void main(String[] args)
    {
        UrlShorten url=new UrlShorten();
        String[] arr={"https://www.google.com","https://www.yahoo.com/","www.gmail.com"};
        for(int i=0;i<arr.length();i++)
        {
            System.out.println("shorter form"+url.shortenUrl(arr[i]));
        }
    }
}
