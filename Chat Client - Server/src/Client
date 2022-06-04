package Chat_room;


import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.InetAddress;
import java.net.Socket;
import java.util.Scanner;
// Y tuong : 1 client gui den server , server se luu lại vao mang , Neu ton tai roi  thi thoi 
// khi server nhan duoc thi server se di phan phat tat ca cac client

// Client ghi thi` ghi cho server thoi 
public class Client {
	private InetAddress host;
	private int port;
	
	public Client(InetAddress host, int port) {
		this.host = host;
		this.port = port;
	}
	
	// Thuc hien 2 cai ham read & write 
	private void execute() throws IOException {
		//Phần bổ sung
		Scanner sc = new Scanner(System.in);
		System.out.print("Nhập vào tên của bạn: ");
		String name = sc.nextLine();
		
		Socket client = new Socket(host, port);
		ReadClient read = new ReadClient(client);
		read.start();
		WriteClient write = new WriteClient(client, name);
		write.start();	
	}
	
	
	public static void main(String[] args) throws IOException {
		Client client = new Client(InetAddress.getLocalHost(), 15797);
		client.execute();
	}
}

class ReadClient extends Thread{
	private Socket client;

	public ReadClient(Socket client) {
		this.client = client;
	}
	
	@Override
	// tat ca lech trong day se duoc thuc thi song song voi cac Threads khac
	public void run() {
		// read
		DataInputStream dis = null;
		try {
			dis = new DataInputStream(client.getInputStream());
			while(true) {
				// read tu server 
				String sms = dis.readUTF();
				// lay ve roi thi` in no ra 
				System.out.println(sms);
			}
		} catch (Exception e) {
			try {
				// neu loi : dong' luong` cua read dulieu 
				dis.close();
				client.close();
				
			} catch (IOException ex) {
				System.out.println("Ngắt kết nối Server");
			}
		}
	}
}

class WriteClient extends Thread{
	private Socket client;
	private String name;

	public WriteClient(Socket client, String name) {
		this.client = client;
		this.name = name;
	}
	
	@Override
	public void run() {
		DataOutputStream dos = null;
		Scanner sc = null;
		try {
			dos = new DataOutputStream(client.getOutputStream());
			sc = new Scanner(System.in);
			while(true) {
				String sms = sc.nextLine();
				// nguoi dung nhap vao thi gưi len server
				dos.writeUTF(name + ": " + sms);
			}
		} catch (Exception e) {
			try {
				dos.close();
				client.close();
			} catch (IOException ex) {
				System.out.println("Ngắt kết nối Server");
			}
		}
	}
	
}
