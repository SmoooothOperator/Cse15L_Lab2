# CSE15L Lab 2
**Part 1** <br>
Code for StringServer: <br>
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String[] arr = new String[2];
    int size;
    
    public void expandCapacity(){
        int currentCapacity = arr.length;
        if(size < currentCapacity){
            return;
        }
        else{
            String [] expanded = new String[currentCapacity*2];
            for(int i = 0; i < this.size; i++){
                expanded[i] = this.arr[i];
            }
            arr = expanded;
        }
    }
    public String format(String[] arr){
        StringBuilder builder = new StringBuilder();
        for(int i = 0; i < size; i++){
            builder.append(arr[i]).append(System.lineSeparator());
        }
        return builder.toString();
    }

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return format(arr);
        }
        else if(url.getPath().equals("/add-message")){
            
                String[] newWord = url.getQuery().split("=");
                String toAdd = String.format("%d. %s", size+1, newWord[1]);
                expandCapacity();
                arr[size] = toAdd;
                size++;

                return "String added!";
                
                

        }
         else {
            
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}


**cd path to directory** <br>
In the home directory <br>
since cd changes the directory, a path to the directory will change the current directory to the one in the path. <br>
![Image](cd2.png) <br>
