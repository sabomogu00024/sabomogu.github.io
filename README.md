<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>営業指標計算ツール</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
        }
        /* スクロールバーのスタイルをカスタマイズ */
        .scroll-container::-webkit-scrollbar {
            width: 8px;
        }
        .scroll-container::-webkit-scrollbar-track {
            background: #e5e7eb;
            border-radius: 10px;
        }
        .scroll-container::-webkit-scrollbar-thumb {
            background: #9ca3af;
            border-radius: 10px;
            border: 2px solid #e5e7eb;
        }
        .scroll-container::-webkit-scrollbar-thumb:hover {
            background: #6b7280;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div class="w-full max-w-4xl p-8 bg-white rounded-2xl shadow-xl space-y-8">
        <h1 class="text-3xl font-bold text-center text-gray-800">営業指標計算ツール</h1>

        <!-- 営業指標セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700 pb-2 border-b">営業指標</h2>
            <!-- 入力フォーム -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Net売り上げ -->
                <div class="flex flex-col space-y-1">
                    <label for="netSales" class="text-sm font-medium text-gray-700">Net売り上げ</label>
                    <input type="number" id="netSales" placeholder="例: 100000" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
                <!-- 組数 -->
                <div class="flex flex-col space-y-1">
                    <label for="customers" class="text-sm font-medium text-gray-700">組数</label>
                    <input type="number" id="customers" placeholder="例: 50" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
                <!-- 労働時間数 -->
                <div class="flex flex-col space-y-1">
                    <label for="workHours" class="text-sm font-medium text-gray-700">労働時間数</label>
                    <input type="number" id="workHours" placeholder="例: 8" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
            </div>
            <!-- 出力フォーム -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
                <div class="bg-gray-100 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-gray-500">客単価</p>
                    <p id="averagePrice" class="text-2xl font-bold text-gray-800">-</p>
                </div>
                <div class="bg-gray-100 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-gray-500">労時売り上げ</p>
                    <p id="salesPerHour" class="text-2xl font-bold text-gray-800">-</p>
                </div>
                <div class="bg-gray-100 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-gray-500">人時接客数</p>
                    <p id="customersPerHour" class="text-2xl font-bold text-gray-800">-</p>
                </div>
            </div>
        </div>

        <!-- 支払い方法セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700 pb-2 border-b">支払い方法</h2>
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
                <div class="flex flex-col space-y-1">
                    <label for="cash" class="text-sm font-medium text-gray-700">現金</label>
                    <input type="number" id="cash" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
                <div class="flex flex-col space-y-1">
                    <label for="credit" class="text-sm font-medium text-gray-700">クレジット</label>
                    <input type="number" id="credit" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
                <div class="flex flex-col space-y-1">
                    <label for="eMoney" class="text-sm font-medium text-gray-700">電子マネー</label>
                    <input type="number" id="eMoney" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
                <div class="flex flex-col space-y-1">
                    <label for="prepayment" class="text-sm font-medium text-gray-700">事前会計</label>
                    <input type="number" id="prepayment" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-4">
                <div class="bg-indigo-50 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-indigo-700">支払い小計</p>
                    <p id="subtotalPayment" class="text-2xl font-bold text-indigo-900">-</p>
                </div>
                <div class="bg-indigo-50 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-indigo-700">総売上</p>
                    <p id="totalSales" class="text-2xl font-bold text-indigo-900">-</p>
                </div>
            </div>
        </div>

        <!-- 在庫・実使用量計算セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700 pb-2 border-b">在庫・実使用量計算</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Mパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">Mパティ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="mpCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="mpLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="mpPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="mpArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="mpLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="mpCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="mpInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="mpUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                <!-- Zパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">Zパティ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="zpCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="zpLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="zpPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="zpArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="zpLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="zpCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="zpInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="zpUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                <!-- Rパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">Rパティ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="rpCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="rpLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="rpPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="rpArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="rpLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="rpCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="rpInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="rpUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                <!-- Mバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">Mバンズ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="mbCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">袋数: <input type="number" id="mbBag" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="mbLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="mbPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="mbArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="mbLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="mbCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="mbInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="mbUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                 <!-- Zバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">Zバンズ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="zbCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">袋数: <input type="number" id="zbBag" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="zbLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="zbPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="zbArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="zbLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="zbCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="zbInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="zbUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                 <!-- クープバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">クープバンズ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">袋数: <input type="number" id="qbBag" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="qbLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="qbPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="qbArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="qbLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="qbCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="qbInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="qbUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
                 <!-- マフィンバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2 flex flex-col">
                    <h3 class="text-lg font-medium text-gray-700">マフィンバンズ</h3>
                    <div class="flex-grow space-y-2">
                        <label class="text-sm text-gray-700">ケース数: <input type="number" id="mCase" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">袋数: <input type="number" id="mBag" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">バラ: <input type="number" id="mLoose" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">前残: <input type="number" id="mPrev" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">入荷: <input type="number" id="mArrival" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                        <label class="text-sm text-gray-700">ロス: <input type="number" id="mLoss" class="w-full rounded-md border-gray-300 shadow-sm p-1 text-sm"></label>
                    </div>
                    <div class="mt-4 pt-2 border-t space-y-2">
                        <div>
                            <p class="text-xs font-medium text-gray-500">ケース在庫:</p>
                            <p id="mCaseInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">在庫:</p>
                            <p id="mInventory" class="text-base font-bold text-gray-800">-</p>
                        </div>
                        <div>
                            <p class="text-xs font-medium text-gray-500">実使用量:</p>
                            <p id="mUsage" class="text-base font-bold text-gray-800">-</p>
                        </div>
                    </div>
                </div>
            </div>
            <!-- 在庫合計使用量セクション -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-6 pt-4 border-t">
                <div class="bg-blue-50 p-4 rounded-lg shadow-sm">
                    <p class="text-sm font-medium text-blue-700">バンズ合計使用量</p>
                    <p id="totalBunUsage" class="text-2xl font-bold text-blue-900">-</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // 計算結果を表示する要素
            const averagePriceSpan = document.getElementById('averagePrice');
            const salesPerHourSpan = document.getElementById('salesPerHour');
            const customersPerHourSpan = document.getElementById('customersPerHour');
            const subtotalPaymentSpan = document.getElementById('subtotalPayment');
            const totalSalesSpan = document.getElementById('totalSales');
            const mpCaseInventorySpan = document.getElementById('mpCaseInventory');
            const mpInventorySpan = document.getElementById('mpInventory');
            const mpUsageSpan = document.getElementById('mpUsage');
            const zpCaseInventorySpan = document.getElementById('zpCaseInventory');
            const zpInventorySpan = document.getElementById('zpInventory');
            const zpUsageSpan = document.getElementById('zpUsage');
            const rpCaseInventorySpan = document.getElementById('rpCaseInventory');
            const rpInventorySpan = document.getElementById('rpInventory');
            const rpUsageSpan = document.getElementById('rpUsage');
            const mbCaseInventorySpan = document.getElementById('mbCaseInventory');
            const mbInventorySpan = document.getElementById('mbInventory');
            const mbUsageSpan = document.getElementById('mbUsage');
            const zbCaseInventorySpan = document.getElementById('zbCaseInventory');
            const zbInventorySpan = document.getElementById('zbInventory');
            const zbUsageSpan = document.getElementById('zbUsage');
            const qbCaseInventorySpan = document.getElementById('qbCaseInventory');
            const qbInventorySpan = document.getElementById('qbInventory');
            const qbUsageSpan = document.getElementById('qbUsage');
            const mCaseInventorySpan = document.getElementById('mCaseInventory');
            const mInventorySpan = document.getElementById('mInventory');
            const mUsageSpan = document.getElementById('mUsage');
            const totalBunUsageSpan = document.getElementById('totalBunUsage');

            // すべての入力要素を取得
            const allInputs = document.querySelectorAll('input[type="number"]');

            // 計算を実行し、結果を表示する関数
            const calculateMetrics = () => {
                // 営業指標
                const netSales = parseFloat(document.getElementById('netSales').value) || 0;
                const customers = parseFloat(document.getElementById('customers').value) || 0;
                const workHours = parseFloat(document.getElementById('workHours').value) || 0;
                
                averagePriceSpan.textContent = customers !== 0 ? (netSales / customers).toFixed(2) : "0では割り算できません";
                salesPerHourSpan.textContent = workHours !== 0 ? (netSales / workHours).toFixed(2) : "0では割り算できません";
                customersPerHourSpan.textContent = workHours !== 0 ? (customers / workHours).toFixed(2) : "0では割り算できません";

                // 支払い方法
                const cash = parseFloat(document.getElementById('cash').value) || 0;
                const credit = parseFloat(document.getElementById('credit').value) || 0;
                const eMoney = parseFloat(document.getElementById('eMoney').value) || 0;
                const prepayment = parseFloat(document.getElementById('prepayment').value) || 0;

                subtotalPaymentSpan.textContent = Math.floor(credit + eMoney + prepayment);
                totalSalesSpan.textContent = Math.floor(cash + credit + eMoney + prepayment);

                // 在庫・実使用量計算
                // Mパティ
                const mpCase = parseFloat(document.getElementById('mpCase').value) || 0;
                const mpLoose = parseFloat(document.getElementById('mpLoose').value) || 0;
                const mpCaseInventory = mpCase * 96;
                const mpInventory = mpCaseInventory + mpLoose;
                mpCaseInventorySpan.textContent = Math.floor(mpCaseInventory);
                mpInventorySpan.textContent = Math.floor(mpInventory);
                const mpPrev = parseFloat(document.getElementById('mpPrev').value) || 0;
                const mpArrival = parseFloat(document.getElementById('mpArrival').value) || 0;
                const mpLoss = parseFloat(document.getElementById('mpLoss').value) || 0;
                const mpUsage = mpPrev + mpArrival - mpInventory - mpLoss;
                mpUsageSpan.textContent = Math.floor(mpUsage);

                // Zパティ
                const zpCase = parseFloat(document.getElementById('zpCase').value) || 0;
                const zpLoose = parseFloat(document.getElementById('zpLoose').value) || 0;
                const zpCaseInventory = zpCase * 64;
                const zpInventory = zpCaseInventory + zpLoose;
                zpCaseInventorySpan.textContent = Math.floor(zpCaseInventory);
                zpInventorySpan.textContent = Math.floor(zpInventory);
                const zpPrev = parseFloat(document.getElementById('zpPrev').value) || 0;
                const zpArrival = parseFloat(document.getElementById('zpArrival').value) || 0;
                const zpLoss = parseFloat(document.getElementById('zpLoss').value) || 0;
                const zpUsage = zpPrev + zpArrival - zpInventory - zpLoss;
                zpUsageSpan.textContent = Math.floor(zpUsage);
                
                // Rパティ
                const rpCase = parseFloat(document.getElementById('rpCase').value) || 0;
                const rpLoose = parseFloat(document.getElementById('rpLoose').value) || 0;
                const rpCaseInventory = rpCase * 90;
                const rpInventory = rpCaseInventory + rpLoose;
                rpCaseInventorySpan.textContent = Math.floor(rpCaseInventory);
                rpInventorySpan.textContent = Math.floor(rpInventory);
                const rpPrev = parseFloat(document.getElementById('rpPrev').value) || 0;
                const rpArrival = parseFloat(document.getElementById('rpArrival').value) || 0;
                const rpLoss = parseFloat(document.getElementById('rpLoss').value) || 0;
                const rpUsage = rpPrev + rpArrival - rpInventory - rpLoss;
                rpUsageSpan.textContent = Math.floor(rpUsage);

                // Mバンズ
                const mbCase = parseFloat(document.getElementById('mbCase').value) || 0;
                const mbBag = parseFloat(document.getElementById('mbBag').value) || 0;
                const mbLoose = parseFloat(document.getElementById('mbLoose').value) || 0;
                const mbCaseInventory = mbCase * 24;
                const mbInventory = mbCaseInventory + mbBag * 6 + mbLoose;
                mbCaseInventorySpan.textContent = Math.floor(mbCaseInventory);
                mbInventorySpan.textContent = Math.floor(mbInventory);
                const mbPrev = parseFloat(document.getElementById('mbPrev').value) || 0;
                const mbArrival = parseFloat(document.getElementById('mbArrival').value) || 0;
                const mbLoss = parseFloat(document.getElementById('mbLoss').value) || 0;
                const mbUsage = mbPrev + mbArrival - mbInventory - mbLoss;
                mbUsageSpan.textContent = Math.floor(mbUsage);

                // Zバンズ
                const zbCase = parseFloat(document.getElementById('zbCase').value) || 0;
                const zbBag = parseFloat(document.getElementById('zbBag').value) || 0;
                const zbLoose = parseFloat(document.getElementById('zbLoose').value) || 0;
                const zbCaseInventory = zbCase * 24;
                const zbInventory = zbCaseInventory + zbBag * 6 + zbLoose;
                zbCaseInventorySpan.textContent = Math.floor(zbCaseInventory);
                zbInventorySpan.textContent = Math.floor(zbInventory);
                const zbPrev = parseFloat(document.getElementById('zbPrev').value) || 0;
                const zbArrival = parseFloat(document.getElementById('zbArrival').value) || 0;
                const zbLoss = parseFloat(document.getElementById('zbLoss').value) || 0;
                const zbUsage = zbPrev + zbArrival - zbInventory - zbLoss;
                zbUsageSpan.textContent = Math.floor(zbUsage);

                // クープバンズ
                const qbBag = parseFloat(document.getElementById('qbBag').value) || 0;
                const qbLoose = parseFloat(document.getElementById('qbLoose').value) || 0;
                const qbCaseInventory = qbBag * 12;
                const qbInventory = qbBag * 12 + qbLoose;
                qbCaseInventorySpan.textContent = Math.floor(qbCaseInventory);
                qbInventorySpan.textContent = Math.floor(qbInventory);
                const qbPrev = parseFloat(document.getElementById('qbPrev').value) || 0;
                const qbArrival = parseFloat(document.getElementById('qbArrival').value) || 0;
                const qbLoss = parseFloat(document.getElementById('qbLoss').value) || 0;
                const qbUsage = qbPrev + qbArrival - qbInventory - qbLoss;
                qbUsageSpan.textContent = Math.floor(qbUsage);
                
                // マフィンバンズ
                const mCase = parseFloat(document.getElementById('mCase').value) || 0;
                const mBag = parseFloat(document.getElementById('mBag').value) || 0;
                const mLoose = parseFloat(document.getElementById('mLoose').value) || 0;
                const mCaseInventory = mCase * 72;
                const mInventory = mCaseInventory + mBag * 6 + mLoose;
                mCaseInventorySpan.textContent = Math.floor(mCaseInventory);
                mInventorySpan.textContent = Math.floor(mInventory);
                const mPrev = parseFloat(document.getElementById('mPrev').value) || 0;
                const mArrival = parseFloat(document.getElementById('mArrival').value) || 0;
                const mLoss = parseFloat(document.getElementById('mLoss').value) || 0;
                const mUsage = mPrev + mArrival - mInventory - mLoss;
                mUsageSpan.textContent = Math.floor(mUsage);

                // バンズ合計使用量
                const totalBunUsage = mbUsage + zbUsage + qbUsage + mUsage;
                totalBunUsageSpan.textContent = Math.floor(totalBunUsage);
            };

            // 全ての入力要素にイベントリスナーを追加して、入力時に計算を再実行する
            allInputs.forEach(input => {
                input.addEventListener('input', calculateMetrics);
            });
            
            // ページロード時に一度計算を実行
            calculateMetrics();
        });
    </script>
</body>
</html>
最終更新日　2025年8月19日
