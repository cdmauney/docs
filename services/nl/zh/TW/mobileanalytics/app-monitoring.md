---

copyright:
  years: 2015, 2016

---
# 使用 {{site.data.keyword.mobileanalytics_short}} 監視應用程式
{: #monitoringapps}
*前次更新：2016 年 5 月 6 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} 提供行動應用程式的監視及分析。您可以記錄用戶端日誌，以及使用 {{site.data.keyword.mobileanalytics_short}} Client SDK 來監視資料。開發人員可以控制何時將這項資料傳送至 {{site.data.keyword.mobileanalytics_short}} 服務。將資料遞送給 {{site.data.keyword.mobileanalytics_short}} 時，您可以使用 {{site.data.keyword.mobileanalytics_short}} 儀表板來深入分析行動應用程式、裝置及用戶端日誌。
{: shortdesc}

## 使用自訂圖表視覺化資料
{: #custom-charts}

您可以視覺化分析儲存庫中收集到的分析資料。此視覺化是一種功能強大的方式，用來檢查特定使用案例的資料。除了您所報告的自訂資料之外，您還可以使用 Operational Analytics 已收集到的資料來建立圖表。

### 建立用戶端日誌的自訂圖表
{: #custom-charts-client-logs}

您可以建立用戶端日誌的自訂圖表，而用戶端日誌包含使用平台的「日誌程式 API」所傳送的日誌資訊。日誌資訊也包括有關裝置的環境定義資訊（包括環境、應用程式名稱及應用程式版本）。

在此範例中，您使用用戶端日誌資料來建立流程圖。最終圖形會顯示特定應用程式中記載層次的分佈。您也有可在圖表中顯示的下列資料：

* 特定資料
  * 記載層次
* 訊息資料
  * 時間戳記
* 裝置 OS 環境定義資料
  * 應用程式名稱
  * 應用程式版本
  * 裝置 OS
* 裝置環境定義資料
  * 裝置 ID
  * 裝置模型
  * 裝置 OS 版本


1. 確定您的應用程式正在收集裝置日誌，或收集分析。
2. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**儀表板**頁面上的**自訂圖表**標籤。您可以根據已傳送至伺服器的分析訊息來建立圖表。
3. 按一下**建立圖表**來建立新的自訂圖表，然後提供下列值：
  * 圖表標題：應用程式及記載層次
  * 事件類型：用戶端日誌
  * 圖表類型：流程圖
5. 按一下**圖表定義**標籤，然後提供下列值：
  * 來源：應用程式名稱
  * 目的地：記載層次
  * 內容：您的應用程式名稱
7. 按一下**儲存**

### 匯出自訂資料
{: #export-custom-data}

您可以將每一個自訂圖表中的資料匯出為 JSON、XML 或 CSV 格式。

匯出資料的結構取決於所匯出的圖表。若要匯出資料，請按一下自訂圖表右上方的匯出圖示。



### 匯出及匯入自訂圖表定義
{: #export-import-custom}

您可以透過程式設計方式，或在「{{site.data.keyword.mobileanalytics_short}} 儀表板」中手動匯入及匯出自訂圖表定義。

請確定您在「{{site.data.keyword.mobileanalytics_short}} 儀表板」中至少有一個自訂圖表。
在此範例中，您可以手動匯出及匯入自訂圖表定義。

1. 在 {{site.data.keyword.mobileanalytics_short}} 主控台中，按一下**儀表板**頁面中的**自訂圖表**標籤。
2. 若要匯出自訂圖表定義，請按一下**匯出圖表**。此動作會顯示用來儲存 `customChartsDefinition.json` 檔案的對話框。
3. 選擇用來儲存檔案的位置。
4. 按一下每一個自訂圖表旁的**刪除圖表**圖示，以刪除所有自訂圖表。
5. 若要匯入自訂圖表定義，請按一下**匯入圖表**。此動作會顯示用來選擇檔案的對話框。
6. 選擇您先前匯出的 `customChartsDefinition.json` 檔案以將它開啟。

您也可以使用選擇的 HTTP 用戶端（例如，CURL 或 postman），透過程式設計方式匯出及匯入自訂圖表定義：
* 進行匯出的 GET 端點是 `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`。
* 進行匯入的 POST 端點是 `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`。

**附註**：如果您匯入已存在的自訂圖表定義，則最終定義會重複，這也表示「{{site.data.keyword.mobileanalytics_short}} 儀表板」會顯示重複的自訂圖表。

## 設定警示
{: #alerts}

您可以在「{{site.data.keyword.mobileanalytics_short}} 主控台」中設定警示定義的臨界值，以更適當地監視您的活動。

您可以配置臨界值，以在超出時，觸發警示來通知「{{site.data.keyword.mobileanalytics_short}} 主控台」監視器。觸發的警示可以在主控台上進行視覺化，或者自訂 Webhook 可以處理警示。此特性提供主動的方法來偵測用戶端日誌錯誤、伺服器日誌錯誤、延長網路延遲期間及鑑別失敗。反應臨界值及警示讓您不需要篩選資料，並且用更廣的精度來設定臨界值。

### 建立用戶端日誌的警示定義
{: #alert-def-client-logs}

您可以根據用戶端日誌來建立警示定義。

在此範例中，您使用用戶端日誌資料來建立警示定義。此警示會監視過去 5 分鐘接收到的所有用戶端日誌，而且除非停用或刪除警示定義，否則會持續每 5 分鐘檢查一次。針對已對相同應用程式名稱及版本傳送 3 個以上用戶端錯誤日誌的每一個裝置，觸發警示。

1. 在「{{site.data.keyword.mobileanalytics_short}} 主控台」中，按一下鈴聲圖示以移至**警示日誌**頁面。
2. 移至**警示管理**頁面，然後按一下**建立警示**。
3. 提供下列值：
	* 警示名稱：用戶端日誌的警示
	* 訊息：錯誤訊息警示
	* 查詢頻率：5 分鐘
	* 事件類型：用戶端日誌
		* 內容：記載層次
			* 值：錯誤
			* 臨界值
				* 臨界值類型：應用程式實例總計

					**附註**：如果您選擇「應用程式平均值」選項，則用戶端日誌會除以裝置數目來取得平均值。例如，如果您有兩個裝置，而且其中一個裝置傳送六個用戶端日誌，而另一個裝置傳送三個用戶端日誌，則平均值是 4.5 個用戶端日誌。
				* 運算子：大於或等於 3<!-- insert alert definition tab image? -->

4. 按**下一步**或**分佈方法**標籤，然後提供下列值：
	* 方法：僅限 Analytics 主控台

		附註：如果您要將具有 JSON 有效負載的 POST 訊息額外傳送至自訂的 URL，請選擇「Analytics 主控台及 Network Post」選項。如果您選擇這個選項，則可以使用下列欄位：
		* Network Post URL
        * 標頭
        * 鑑別類型
5. 按一下**儲存**。

您已建立警示定義，以在用戶端日誌數目達到 3 個以上錯誤日誌的臨界值時，於每 5 分鐘間隔結束時觸發警示。

### 建立應用程式損毀的警示定義
{: #alert-def-app-crash}

您可以根據應用程式損毀來建立警示定義。

在此範例中，您使用應用程式損毀資料來建立警示定義。此警示會監視過去 2 分鐘的所有應用程式損毀，而且除非停用或刪除警示定義，否則會持續每 2 分鐘檢查一次。針對每一個損毀 5 次以上的應用程式，觸發警示。如需應用程式損毀的相關資訊，請參閱[應用程式損毀](app_crash/c_op_analytics_crashes.html)。

1. 在「{{site.data.keyword.mobileanalytics_short}} 主控台」中，按一下**警示**圖示。此動作會啟動「警示日誌」頁面。
2. 按一下**警示管理**標籤，然後按一下**建立警示**。
3. 提供下列值：
	* 警示名稱：應用程式損毀的警示
	* 訊息：應用程式損毀警示
	* 查詢頻率：應用程式損毀
		* 應用程式名稱：任何應用程式
		* 應用程式版本：任何版本
    * 臨界值
      * 臨界值類型：損毀計數
      * 運算子：大於或等於 5
4. 按一下**分佈方法**標籤，然後提供下列值：
  * 方法：僅限 Analytics 主控台

    **附註**：如果您要將具有 JSON 有效負載的 POST 訊息額外傳送至自訂的 URL，請選擇 **Analytics 主控台及 Network Post** 選項。如果您選擇這個選項，則可以使用下列欄位：
      * Network Post URL（必要）
      * 標頭（選用）
      * 鑑別類型（必要）
5. 按一下**儲存**。

### 管理警示定義
{: #managing-alert-definitions}

在此範例中，您從「警示管理」頁面中管理警示定義。

1. 在「{{site.data.keyword.mobileanalytics_short}} 主控台」中，按一下**警示**圖示。此動作會開啟「警示日誌」頁面。
2. 按一下**警示管理**標籤。
3. 選用項目：切換**已啟用**直欄下方的勾選框，以啟用或停用特定警示定義。
4. 選用項目：如果您要建立警示定義的副本，並變更某些值，請按一下**複製**圖示。
5. 選用項目：如果您要編輯警示定義，請按一下**鉛筆**圖示。
6. 選用項目：如果您要刪除警示定義，請按一下**垃圾桶**圖示。

### 檢視警示詳細資料
{: #viewing-alert-details}

在此範例中，您從「警示日誌」頁面中檢視已觸發警示的詳細資料。

1. 在「{{site.data.keyword.mobileanalytics_short}} 主控台」中，按一下**警示**圖示。此動作會啟動「警示日誌」頁面。
2. 按一下任何警示的 **+** 圖示。此動作會顯示**警示定義**及**警示實例**區段。

    **附註**：如果未刪除或修改對應的警示定義，您可以按一下**編輯警示**來編輯警示定義。否則，**編輯警示**按鈕無法使用，並且會顯示下列訊息：

    `已修改或刪除此警示定義。`

3. 選用項目：選取警示，然後按一下**垃圾桶**圖示來刪除警示。

## 應用程式損毀
{: #monitor-app-crash}

您可以在「{{site.data.keyword.mobileanalytics_short}} 主控台」中檢視應用程式損毀的相關資訊，以更適當地監視應用程式並進行疑難排解。

### 應用程式損毀監視
{: #app-crash}

您可以在「{{site.data.keyword.mobileanalytics_short}} 主控台」的**儀表板**區段中快速查看應用程式損毀的相關資訊。

在**儀表板**區段的**概觀**頁面中，**損毀**長條圖會顯示一段時間的損毀的直方圖。

您可以使用兩種方式來顯示資料：

1. 顯示損毀比率：一段時間的損毀比率
2. 顯示損毀總計：一段時間的損毀總計


### 應用程式損毀疑難排解
{: #app-crash-troubleshooting}

您可以檢視「{{site.data.keyword.mobileanalytics_short}} 主控台」的**應用程式**區段中的**損毀**頁面，以更適當地管理應用程式。

**損毀概觀**表格會顯示下列資料直欄：

* 應用程式：應用程式名稱
* 損毀：該應用程式的損毀總數
* 使用總計：使用者開啟及關閉該應用程式的總次數
* 損毀比率：每次使用的損毀百分比

**損毀摘要**表格可進行排序，而且包括下列資料直欄：

* 損毀
* 裝置
* 前次損毀
* 應用程式
* OS
* 訊息

您可以按一下任何項目旁的 + 圖示來顯示**損毀詳細資料**表格，其中包括下列直欄：

* 損毀時間
* 應用程式版本
* OS 版本
* 裝置模型
* 裝置 ID
* 下載：下載已導致損毀的日誌的鏈結

您可以展開**損毀詳細資料**表格中的任何項目來取得更多詳細資料（包括堆疊追蹤）。

**附註**：**損毀摘要**表格的資料是透過查詢嚴重層次用戶端日誌來移入。如果您的應用程式未收集嚴重用戶端日誌，則沒有可用的資料。

