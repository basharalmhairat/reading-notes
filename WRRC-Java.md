#  WRRC and Java
## The Lifecycle of an HTTP request

 ![1_4SEvcz6KvyaqOqBpJABTBg](https://user-images.githubusercontent.com/97823170/158139211-78c2dfee-fd2e-47c6-84ff-354bdff9a269.png)
 
 
 - Differently than with other web languages, like for instance PHP that runs as a module in Apache, Node.js comes with a web server built in.
 -  So Express is actually a hypertext transfer protocol, in short HTTP server. As such I think it doesn’t harm if we quickly cover how HTTP actually works.
 -   HTTP is a quite simple text-based protocol. I use Telnet to show what’s going on behind the scenes when you request a file in the browser.
 -  Don’t be intimidated by what you see on the screen right now.
so in simple words  First I connect to the server, exe Google.com on port 80.That’s the standard HTTP port.
If the request should be encrypted, you would use port 443,which you know as HTTPS in your browser.
Your browser knows this and selects the right portdepending on if you use HTTP or HTTPS.
My local system will now make a call to the domain name service, which resolves the domain name to an IP address.
Once it knows it, it will try to connect to this IP address on port 80, and the system will hopefully reply that we are now connected.

then actual HTTP protocol starts.
I type GET /, which means give me the index page of this web server.
The web server will first tell me if the request went through successfully.
It communicates this by HTTP status code, in this case 200, which means okay.
Then the server replies with a bunch of headers that instruct the browser to do specific things, like setting a cookie and the html, which is quite a lot when it comes to Google.

source:https://medium.com/@officialrahulmandal/the-lifecycle-of-an-http-request-f6b1c1635312

## Do a Simple HTTP Request in Java

![1_H9X3ox7LviQoxLBQcfx1CQ](https://user-images.githubusercontent.com/97823170/158143177-3bfa4a48-e4c7-495e-82b1-0155a15cf984.png)
this photo shows in siple and clear way how it goes for HTTP

Below are the steps we need to follow for sending Java HTTP requests using HttpURLConnection class:

- Create URL object from the GET/POST URL String.
- Call openConnection() method on URL object that returns instance of HttpURLConnection
- Set the request method in HttpURLConnection instance, default value is GET.
- Call setRequestProperty() method on HttpURLConnection instance to set request header values, such as “User-Agent” and “Accept-Language” etc.
- We can call getResponseCode() to get the response HTTP code. This way we know if the request was processed successfully or there was any HTTP error message thrown.
- For GET, we can simply use Reader and InputStream to read the response and process it accordingly.
- For POST, before we read response we need to get the OutputStream from HttpURLConnection instance and write POST parameters into it.
HttpURLConnection Example:
```
HttpURLConnectionExample.java code:

package web;

import com.google.gson.Gson;

import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;

public class App {
    public static void main(String[] args) throws IOException {
        // prework build the JAVA objects that will hold the JSON data

        // step  1 go to the internet and get the JSON data
        // make a url for the API
        URL pokeUrl = new URL("https://pokeapi.co/api/v2/pokemon/ditto");

        // making a connection to the API
        HttpURLConnection pokeHttpURLConnection = (HttpURLConnection) pokeUrl.openConnection();

        // specify the method for the connection
        pokeHttpURLConnection.setRequestMethod("GET");

        // Read the response from the API and save in a string variable
        InputStreamReader pokeInputStreamReader = new InputStreamReader(pokeHttpURLConnection.getInputStream());
        BufferedReader pokeBufferedReader = new BufferedReader(pokeInputStreamReader);
        String pokeData = pokeBufferedReader.readLine();
        System.out.println(pokeData);

        // step 2 same as last week parse the json data into objects using GSON
        // we need to convert the data to Java objects using GSON
        Gson gson = new Gson();
        Pokemon ditto = gson.fromJson(pokeData, Pokemon.class);

        System.out.println(ditto);

        // save the response from the API to a file
        File dittoFile = new File("./ditto.json");
        try (FileWriter dittoFileWriter = new FileWriter(dittoFile)) {
            gson.toJson(ditto, dittoFileWriter);
        }
    }
}
```

Just compare it with the browser HTTP response and you will see that it’s same. You can also save response into any HTML file and open it to compare the responses visually.

