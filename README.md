# 在Colab中自動更新LineBot的WebhookURL
使用colab來執行Linebot是一個好選擇，不須建立Python環境，只須使用pyngrok進行轉址就可以馬上實做，不過實做過得夥伴應該感覺到有一個很大的麻煩就是必須手動更新Webhook URL，每次服務啟動都會被pyngrok更換新網址，然後我們再把網址貼到Line Console 里做測試，這樣流程一兩次也還好，當我們測試程式時，幾乎改一行就要測試一次，一堂課下來可能要處理好幾十次，說累是還好，就是經常忘記，導致服務沒串接。
現在呢？我幫大家解決了，這隻程式可以自主去更新你的Line Bot的Webhook URL，原理很簡單，LINE在年初開放了PUT URL的功能，但是知道的人可能不多，我這裡就把他做好了。

這隻程式的另外一個特色就是用到了多執行緒，原因是pyngrok的網址必須要app.run()執行後幾秒後才會產生，而一般app.run()後，我們是沒辦法執行任何程式的，所以這裡我用的多執行緒，先建立一個執行緒準備去讀取新網址，然後定義他五秒後啟動，再執行app.run()，所以就可以在pyngrok產生後，由剛剛建立好的執行緒去取得新網址，並PUT到Line的控制台。
![image](https://github.com/youjunjer/AutoUpdate_LineBot_WebhookURL/assets/40359899/72bbfbf9-f376-4005-825d-9f0bb0d5f9a3)
