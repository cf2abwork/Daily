## Date : 2026/04/13


**FortiGate Firewall - How to Fix Blocking of WebResource.axd**

## 1. 問題描述 / Problem Description

**繁體中文：**  
FortiGate 預設的 Web Application Firewall (WAF) 設定中，簽名 **90240001**（Known Exploits）會阻擋或記錄包含 `WebResource.axd` 或 `ScriptResource.axd` 的請求。這是因為該簽名原本用來防止攻擊者透過 ASP.NET 嵌入資源進行攻擊，但對正常運作的 ASP.NET 網站（特別是使用 AJAX、Telerik、DevExpress 等控件的網站）會造成嚴重誤報（False Positive）。

**English:**  
In the default Web Application Firewall (WAF) profile of FortiGate, signature **90240001** (Known Exploits) blocks or logs requests containing `WebResource.axd` or `ScriptResource.axd`. This signature was designed to prevent attackers from accessing embedded ASP.NET resources, but it frequently causes false positives on legitimate ASP.NET applications that use AJAX, Telerik, DevExpress, or other UI controls.

**預設行為 / Default Behavior**  
- FortiGate 預設 WAF Profile（default）會對 **90240001** 等 Known Exploits 簽名採取 **Block** 或 **Passthrough + Log** 動作。  
- 許多 ASP.NET 網站因此無法正常載入 JavaScript、CSS 或驗證資源。



## 2. 常見高誤報簽名與意義 / Common High False-Positive Signatures

| Signature ID   | 英文說明 (English Description)                                                                 | 繁體中文說明                                                                 | 誤報機率 |
|----------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|----------|
| **90240001**   | Prevents attackers from accessing embedded resources through URL with "WebResource.axd" or "ScriptResource.axd". | 防止攻擊者透過含有 WebResource.axd 或 ScriptResource.axd 的 URL 存取嵌入式資源。 | 極高     |
| **80080005**   | Generic / Known Exploits detection on dynamic ASP.NET requests.                               | 通用已知攻擊檢測（常見於 ASP.NET 動態請求）。                               | 高       |
| **80200001**   | Generic attack pattern or parameter anomaly.                                                  | 通用攻擊模式或參數異常檢測。                                                 | 高       |
| **60030001**   | Constraint on file extension or resource access (often .axd).                                 | 檔案副檔名或資源存取限制（常與 .axd 相關）。                                 | 高       |
| **60120001**   | HTTP request structure anomaly (length, encoding, etc.).                                      | HTTP 請求結構異常（長度、編碼等）。                                          | 中高     |
| **80080003**   | Similar to 80080005 – dynamic resource or injection related.                                  | 類似 80080005，常見動態資源或注入類誤報。                                    | 高       |
| **90410001**   | Extended Known Exploits detection.                                                            | 擴展的已知攻擊檢測。                                                         | 高       |
| **90410002**   | Extended Known Exploits detection (related series).                                           | 擴展的已知攻擊檢測（同系列）。                                               | 高       |

---

## 3. Default value for fortigate  Fortigate 的預設值


Default value for fortigate

```bash
config waf profile

    edit "default"
          config signature
             set disabled-signature 80080005 80200001 60030001 60120001 80080003 90410001 90410002
          end
    next
end
```



## 3. 建議設定指令

使用以下 CLI 指令，將所有常見誤報簽名加入禁用清單（包含 **90240001**）：

```bash
 
config waf profile
    edit default             
        config signature
            set disabled-signature 90240001 80080005 80200001 60030001 60120001 80080003 90410001 90410002
        end
    next
end
```


