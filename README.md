# 資料來源
本專案資料來自
* 「公開資訊觀測站」2013-2016公司財報, 經由「2017 g0v公民科技創新獎助金計劃」整理彙整
* 環保署或各縣市環保局開發的裁罰記錄, 經由「透明足跡」整理彙整.

# 資料說明
* csv: 原始資料, 欄位包含
    * 基本資料: 年份(year), 財報公司台灣股票代號(stock), 母公司(source), 子公司(target), 母公司持股比例(sublist.holder), 子公司所在國家(sublist.location), 母公司統一編號(taxcode.source), 子公司統一編號(taxcode.target)
    * 資料出處: 母公司是否為財報公司(sublist.is_coreSource), 資料表格出處(sublist.table_source1-列入合併財務報表之子公司, sublist.table_source2-被投資公司名稱, sublist.table_source3-轉投資大陸地區之事業, sublist.table_source4-核心公司董監事及法人代表), 發行方式(market:上市, 上櫃, 興櫃, 公開發行)
    * 其他: 大陸地區表格註解(china.note), 人工處理註記(X1, 修正), 非集團的控股公司(非集團, 標註1為非集團,例如投資銀行、政府機關)
* list.json: 結合「透明足跡」裁罰記錄
   * company_summery: 集團代號(group_no), 集團名稱(group_name), 集團公司數量(company_amount), 集團是否有裁罰記錄(has_fine), 集團內有裁罰記錄的公司數量(fine_company_amount), 集團裁罰記錄數量(fine_record_num), 集團裁罰金額(fine_penalty_amount)
   * company_list:集團內公司關係表(taxcode_source, source, taxcode_target, target, holder)
   * fine_company_list: 集團內有裁罰記錄的公司列表(name, taxcode, penalty_amount, fine_num)
   * target_list: 集團內子公司列表(taxcode, source_list(holder, name))
* graph.json: 整理為d3畫圖格式
   * nodes: taxcode, no_holder, is_core, source (holder, name)
   * links: holder, target(node_index), source (node_index)

# 關係圖呈現
 * https://thaubing.gcaa.org.tw/companydata/graph.html?year={year}&group={group_no}
 * year: 2013-2016
 * group_no: 資料夾名稱, Ex: G1301
 * 開源碼: 
   * git@github.com:starsdog/thaubing_UI.git

# 關係圖說明
* 圖示種類
  * <img height=50 src=https://cdn.rawgit.com/starsdog/openGroups/master/image/core_factory.png>: 核心公司為在台灣上市, 上櫃, 興櫃或公開發行的公司 
  * <img height=50 src=https://cdn.rawgit.com/starsdog/openGroups/master/image/tw_factory.png>: 台灣公司為在台灣登記, 有統一編號的公司
  * <img height=50 src=https://cdn.rawgit.com/starsdog/openGroups/master/image/other_factory.png>: 非台灣公司為在台灣財政部查不到統一編號的公司,
  可能未在台灣登記, 或是登記公司名稱與財報出現名稱不一致, 無法透過名稱比對, 找到統一編號.
  * <img height=50 src=https://cdn.rawgit.com/starsdog/openGroups/master/image/no_holder_factory.png>: 所有母公司持股為零公司為在財報中出現,
  但每個母公司的持股比例皆為零的公司. 
  
* 點選圖示, 出現公司基本資料
  * 統一編號
  * 列出持有該公司股份的母公司名稱與持股比例.
  * 持股比例為"NA": 該資料由「董監事持股餘額明細資料」取得, 該資料未公布持股.

* 關係圖裡線的箭頭方向為母公司指向子公司. 
* 關係圖裡線的長短, 遠近與持股比例無關, 為程式自動編排.

# 問題回報
如果你發現任何問題, 請回報至此專案的issue list


