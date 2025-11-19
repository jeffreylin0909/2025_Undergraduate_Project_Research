# 2025_Undergraduate_Project_Research

  專題研究提出改善 ma-QAOA 配 Adam 解 BBV (Barrat–Barthelemy–Vespignani) 網絡的
Max-Cut 問題時遇到的特定問題。因為 BBV 網絡的特性，其節點之加權度數 (即其與相臨之
邊的權重總和) 具有兩極分布的特性。依據實驗發現，ma-QAOA 之 bata 參數的梯度訊號 (以
gradient variance 表示) 和其控制的節點之度數高度相關，可見該電路參數之梯度訊號也呈兩
極分布。根據文獻顯示，參數之梯度訊號分布不均可能造成數值優化器收斂困難。針對該現
象，我提出了兩種改良手法：參數分組與 Adam 動量重置，以避免梯度訊號不平衡造成的訓
練困難。
  我在 PennyLane lightning.gpu 模擬器上選擇 shots=None (即期望值直接靠 statevector 統計模
擬，而非照機率抽樣) 的裝置實作 ma-QAOA，並以 Pytorch 的 Adam 優化器對 ma-QAOA 輸
出之期望值進行參數訓練。針對節點數量為 12、15、18 的隨機 BBV 網絡，各生成 20 個實
例，每個實例進行 100 組隨機初始化參數，統計其 approximation ratio 與收斂步數。結果顯
示，參數分組與動量重置皆能顯著提升 approximation ratio，且同時使用時有疊加效果；在收
斂速度方面，動量重置能大幅降低收斂步數，而參數分組在動量重置的情況下增加收斂步
數，但在不動量重置的情況下減少收斂步數。本研究提供證據顯示，用 ma-QAOA 搭配 Adam
解 BBV 網絡的 Max-Cut 問題時，因該電路參數梯度訊號的兩極分布，階段參數分組與 Adam
動量重置可提升表現與效率。
