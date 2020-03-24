using System;
using System.IO;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;


namespace test
{
    public class Program
    {
        public static async Task Main(string[] args)
        {
            System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12
                | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls;
            try
            {
                // Create a request for the URL.   
                WebRequest request = WebRequest.Create("http://mysecretUrl.com?parameter=valueParameter");
                // If required by the server, set the credentials.  
                request.Credentials = CredentialCache.DefaultCredentials;
                request.Method = "GET";
                request.Headers.Add(HttpRequestHeader.Authorization, "token MySecretToken");
                request.UseDefaultCredentials = false;
                // Get the response.  
                WebResponse response = request.GetResponse();  //return 401
                                                               // Display the status.  
                Console.WriteLine(((HttpWebResponse)response).StatusDescription);

                // Get the stream containing content returned by the server. 
                // The using block ensures the stream is automatically closed. 
                using (Stream dataStream = response.GetResponseStream())
                {
                    // Open the stream using a StreamReader for easy access.  
                    StreamReader reader = new StreamReader(dataStream);
                    // Read the content.  
                    string responseFromServer = reader.ReadToEnd();
                    // Display the content.  
                    Console.WriteLine(responseFromServer);
                }

                // Close the response.  
                response.Close();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
            var client = new HttpClient();
            try
            {
                
                client.BaseAddress = new Uri("http://mysecretUrl.com?parameter=valueParameter");
                client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("token", "MySecretToken");

                var ret = await client.GetAsync("http://mysecretUrl.com?parameter=valueParameter"); //return 401

            }
            catch (Exception ex)
            {
                Console.WriteLine("Segunda tentativa");
            }

            try
            {
                var requestMessage = new HttpRequestMessage(HttpMethod.Get, "http://mysecretUrl.com?parameter=valueParameter");
                requestMessage.Headers.Authorization = new AuthenticationHeaderValue("token", "MySecretToken");
                var ret2 = await client.SendAsync(requestMessage); //return 401
            }
            catch (Exception ex)
            {
                Console.WriteLine("Terceira tentativa");
            }
        }
    }
}
