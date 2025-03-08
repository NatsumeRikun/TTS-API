# TTS-API
 อ่านข้อความด้วยเสียงแบบแลกแต้ม
 อันนี้คลิปตัวอย่างนะครับ https://youtu.be/oiJ9zmIeJJA

 ใช้ Streamer.bot ในการเชื่อมนะครับ อย่างแรกเราต้องทำแลกแต้มแบบกรอกข้อความมาก่อน
 
 ![image](https://github.com/user-attachments/assets/253f4ae4-38dd-49e2-93ce-748fdd1f1b79)

 จากนั้นเราก็เพิ่ม Actions ใน Streamer.bot
 ![image](https://github.com/user-attachments/assets/9c8a394a-e13d-4878-a43f-be0fa57bc7ec)

 เสร็จแล้วให้เราเพิ่ม Triggers เลือก Twitch -> Channel Reward ->  Reward Redemption -> เลือกชื่อแต้มที่เราสร้าง
 ![image](https://github.com/user-attachments/assets/9ed13376-0016-4014-9ff6-868865545fe4)
 
 แล้วนำโค้ดนี้ไปใส่ 

 ```using System;
    using System.Net.Http;
    using System.Threading.Tasks;
    
    public class CPHInline
    {
        private static readonly HttpClient client = new HttpClient();
    
        public bool Execute()
        {
            string username = args["userName"].ToString();
            string reward = args["rewardName"].ToString();
            string message = args["rawInput"].ToString();
    
            Task.Run(async () => await SendApiRequest()).Wait();
    
            return true;
        }
    
        private async Task SendApiRequest()
        {
            string message = args["rawInput"].ToString();
            string url = "http://localhost:5000/tts/" + Uri.EscapeDataString(message);
    
            try
            {
                HttpResponseMessage response = await client.GetAsync(url);
                
                if (response.IsSuccessStatusCode)
                {
    
                    string responseBody = await response.Content.ReadAsStringAsync();
                }
            }
            catch (Exception ex){}
        }
    }
```

   จากนั้นก็เปิดโปรแกรมที่โหลดมา ก็เป็นอันเสร็จ
   ถ้าใช้ไม่ได้ มีปัญหาแจ้งผมมาได้เลยนะครับ [@Natsume Rikun](https://discordapp.com/users/1058988121972281395)
