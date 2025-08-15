<!DOCTYPE html>
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
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div class="w-full max-w-4xl p-8 bg-white rounded-2xl shadow-xl space-y-8">
        <h1 class="text-3xl font-bold text-center text-gray-800">営業指標計算ツール</h1>

        <!-- 営業指標セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700 pb-2 border-b">営業指標</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Net売り上げ -->
                <div class="flex flex-col space-y-1">
                    <label for="netSales" class="text-sm font-medium text-gray-700">Net売り上げ</label>
                    <input type="number" id="netSales" placeholder="例: 100000" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                    <div class="bg-gray-100 p-2 rounded-md mt-2">
                        <p class="text-xs font-medium text-gray-500">客単価</p>
                        <p id="averagePrice" class="text-base font-bold text-gray-800">-</p>
                    </div>
                </div>
                <!-- 組数 -->
                <div class="flex flex-col space-y-1">
                    <label for="customers" class="text-sm font-medium text-gray-700">組数</label>
                    <input type="number" id="customers" placeholder="例: 50" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                    <div class="bg-gray-100 p-2 rounded-md mt-2">
                        <p class="text-xs font-medium text-gray-500">労時売り上げ</p>
                        <p id="salesPerHour" class="text-base font-bold text-gray-800">-</p>
                    </div>
                </div>
                <!-- 労働時間数 -->
                <div class="flex flex-col space-y-1">
                    <label for="workHours" class="text-sm font-medium text-gray-700">労働時間数</label>
                    <input type="number" id="workHours" placeholder="例: 8" class="w-full rounded-md border-gray-300 shadow-sm p-2 text-sm focus:border-indigo-500 focus:ring-indigo-500">
                    <div class="bg-gray-100 p-2 rounded-md mt-2">
                        <p class="text-xs font-medium text-gray-500">人時接客数</p>
                        <p id="customersPerHour" class="text-base font-bold text-gray-800">-</p>
                    </div>
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

            // 入力要素
            const netSalesInput = document.getElementById('netSales');
            const customersInput = document.getElementById('customers');
            const workHoursInput = document.getElementById('workHours');
            const cashInput = document.getElementById('cash');
            const creditInput = document.getElementById('credit');
            const eMoneyInput = document.getElementById('eMoney');
            const prepaymentInput = document.getElementById('prepayment');
            
            const mpCaseInput = document.getElementById('mpCase');
            const mpLooseInput = document.getElementById('mpLoose');
            const mpPrevInput = document.getElementById('mpPrev');
            const mpArrivalInput = document.getElementById('mpArrival');
            const mpLossInput = document.getElementById('mpLoss');

            const zpCaseInput = document.getElementById('zpCase');
            const zpLooseInput = document.getElementById('zpLoose');
            const zpPrevInput = document.getElementById('zpPrev');
            const zpArrivalInput = document.getElementById('zpArrival');
            const zpLossInput = document.getElementById('zpLoss');

            const rpCaseInput = document.getElementById('rpCase');
            const rpLooseInput = document.getElementById('rpLoose');
            const rpPrevInput = document.getElementById('rpPrev');
            const rpArrivalInput = document.getElementById('rpArrival');
            const rpLossInput = document.getElementById('rpLoss');

            const mbCaseInput = document.getElementById('mbCase');
            const mbBagInput = document.getElementById('mbBag');
            const mbLooseInput = document.getElementById('mbLoose');
            const mbPrevInput = document.getElementById('mbPrev');
            const mbArrivalInput = document.getElementById('mbArrival');
            const mbLossInput = document.getElementById('mbLoss');

            const zbCaseInput = document.getElementById('zbCase');
            const zbBagInput = document.getElementById('zbBag');
            const zbLooseInput = document.getElementById('zbLoose');
            const zbPrevInput = document.getElementById('zbPrev');
            const zbArrivalInput = document.getElementById('zbArrival');
            const zbLossInput = document.getElementById('zbLoss');

            const qbBagInput = document.getElementById('qbBag');
            const qbLooseInput = document.getElementById('qbLoose');
            const qbPrevInput = document.getElementById('qbPrev');
            const qbArrivalInput = document.getElementById('qbArrival');
            const qbLossInput = document.getElementById('qbLoss');

            const mCaseInput = document.getElementById('mCase');
            const mBagInput = document.getElementById('mBag');
            const mLooseInput = document.getElementById('mLoose');
            const mPrevInput = document.getElementById('mPrev');
            const mArrivalInput = document.getElementById('mArrival');
            const mLossInput = document.getElementById('mLoss');

            // 全ての入力フィールドを配列にまとめる
            const allInputs = [
                netSalesInput, customersInput, workHoursInput,
                cashInput, creditInput, eMoneyInput, prepaymentInput,
                mpCaseInput, mpLooseInput, mpPrevInput, mpArrivalInput, mpLossInput,
                zpCaseInput, zpLooseInput, zpPrevInput, zpArrivalInput, zpLossInput,
                rpCaseInput, rpLooseInput, rpPrevInput, rpArrivalInput, rpLossInput,
                mbCaseInput, mbBagInput, mbLooseInput, mbPrevInput, mbArrivalInput, mbLossInput,
                zbCaseInput, zbBagInput, zbLooseInput, zbPrevInput, zbArrivalInput, zbLossInput,
                qbBagInput, qbLooseInput, qbPrevInput, qbArrivalInput, qbLossInput,
                mCaseInput, mBagInput, mLooseInput, mPrevInput, mArrivalInput, mLossInput
            ];

            // 計算を実行し、結果を表示する関数
            const calculateMetrics = () => {
                // 営業指標
                const netSales = parseFloat(netSalesInput.value) || 0;
                const customers = parseFloat(customersInput.value) || 0;
                const workHours = parseFloat(workHoursInput.value) || 0;
                
                averagePriceSpan.textContent = customers !== 0 ? (netSales / customers).toFixed(2) : "0では割り算できません";
                salesPerHourSpan.textContent = workHours !== 0 ? (netSales / workHours).toFixed(2) : "0では割り算できません";
                customersPerHourSpan.textContent = workHours !== 0 ? (customers / workHours).toFixed(2) : "0では割り算できません";

                // 支払い方法
                const cash = parseFloat(cashInput.value) || 0;
                const credit = parseFloat(creditInput.value) || 0;
                const eMoney = parseFloat(eMoneyInput.value) || 0;
                const prepayment = parseFloat(prepaymentInput.value) || 0;

                subtotalPaymentSpan.textContent = Math.floor(credit + eMoney + prepayment);
                totalSalesSpan.textContent = Math.floor(cash + credit + eMoney + prepayment);

                // 在庫・実使用量計算
                // Mパティ
                const mpCase = parseFloat(mpCaseInput.value) || 0;
                const mpLoose = parseFloat(mpLooseInput.value) || 0;
                const mpCaseInventory = Math.floor(mpCase * 96);
                const mpInventory = Math.floor(mpCaseInventory + mpLoose);
                mpCaseInventorySpan.textContent = mpCaseInventory;
                mpInventorySpan.textContent = mpInventory;
                const mpPrev = parseFloat(mpPrevInput.value) || 0;
                const mpArrival = parseFloat(mpArrivalInput.value) || 0;
                const mpLoss = parseFloat(mpLossInput.value) || 0;
                mpUsageSpan.textContent = Math.floor(mpPrev + mpArrival - mpInventory - mpLoss);

                // Zパティ
                const zpCase = parseFloat(zpCaseInput.value) || 0;
                const zpLoose = parseFloat(zpLooseInput.value) || 0;
                const zpCaseInventory = Math.floor(zpCase * 64);
                const zpInventory = Math.floor(zpCaseInventory + zpLoose);
                zpCaseInventorySpan.textContent = zpCaseInventory;
                zpInventorySpan.textContent = zpInventory;
                const zpPrev = parseFloat(zpPrevInput.value) || 0;
                const zpArrival = parseFloat(zpArrivalInput.value) || 0;
                const zpLoss = parseFloat(zpLossInput.value) || 0;
                zpUsageSpan.textContent = Math.floor(zpPrev + zpArrival - zpInventory - zpLoss);
                
                // Rパティ
                const rpCase = parseFloat(rpCaseInput.value) || 0;
                const rpLoose = parseFloat(rpLooseInput.value) || 0;
                const rpCaseInventory = Math.floor(rpCase * 90);
                const rpInventory = Math.floor(rpCaseInventory + rpLoose);
                rpCaseInventorySpan.textContent = rpCaseInventory;
                rpInventorySpan.textContent = rpInventory;
                const rpPrev = parseFloat(rpPrevInput.value) || 0;
                const rpArrival = parseFloat(rpArrivalInput.value) || 0;
                const rpLoss = parseFloat(rpLossInput.value) || 0;
                rpUsageSpan.textContent = Math.floor(rpPrev + rpArrival - rpInventory - rpLoss);
                
                // Mバンズ
                const mbCase = parseFloat(mbCaseInput.value) || 0;
                const mbBag = parseFloat(mbBagInput.value) || 0;
                const mbLoose = parseFloat(mbLooseInput.value) || 0;
                const mbCaseInventory = Math.floor(mbCase * 24);
                const mbInventory = Math.floor(mbCaseInventory + mbBag * 6 + mbLoose);
                mbCaseInventorySpan.textContent = mbCaseInventory;
                mbInventorySpan.textContent = mbInventory;
                const mbPrev = parseFloat(mbPrevInput.value) || 0;
                const mbArrival = parseFloat(mbArrivalInput.value) || 0;
                const mbLoss = parseFloat(mbLossInput.value) || 0;
                mbUsageSpan.textContent = Math.floor(mbPrev + mbArrival - mbInventory - mbLoss);

                // Zバンズ
                const zbCase = parseFloat(zbCaseInput.value) || 0;
                const zbBag = parseFloat(zbBagInput.value) || 0;
                const zbLoose = parseFloat(zbLooseInput.value) || 0;
                const zbCaseInventory = Math.floor(zbCase * 24);
                const zbInventory = Math.floor(zbCaseInventory + zbBag * 6 + zbLoose);
                zbCaseInventorySpan.textContent = zbCaseInventory;
                zbInventorySpan.textContent = zbInventory;
                const zbPrev = parseFloat(zbPrevInput.value) || 0;
                const zbArrival = parseFloat(zbArrivalInput.value) || 0;
                const zbLoss = parseFloat(zbLossInput.value) || 0;
                zbUsageSpan.textContent = Math.floor(zbPrev + zbArrival - zbInventory - zbLoss);

                // クープバンズ
                const qbBag = parseFloat(qbBagInput.value) || 0;
                const qbLoose = parseFloat(qbLooseInput.value) || 0;
                // クープバンズのケース在庫は袋数から計算
                const qbCaseInventory = Math.floor(qbBag * 12);
                const qbInventory = Math.floor(qbCaseInventory + qbLoose);
                qbCaseInventorySpan.textContent = qbCaseInventory;
                qbInventorySpan.textContent = qbInventory;
                const qbPrev = parseFloat(qbPrevInput.value) || 0;
                const qbArrival = parseFloat(qbArrivalInput.value) || 0;
                const qbLoss = parseFloat(qbLossInput.value) || 0;
                qbUsageSpan.textContent = Math.floor(qbPrev + qbArrival - qbInventory - qbLoss);
                
                // マフィンバンズ
                const mCase = parseFloat(mCaseInput.value) || 0;
                const mBag = parseFloat(mBagInput.value) || 0;
                const mLoose = parseFloat(mLooseInput.value) || 0;
                const mCaseInventory = Math.floor(mCase * 72);
                const mInventory = Math.floor(mCaseInventory + mBag * 6 + mLoose);
                mCaseInventorySpan.textContent = mCaseInventory;
                mInventorySpan.textContent = mInventory;
                const mPrev = parseFloat(mPrevInput.value) || 0;
                const mArrival = parseFloat(mArrivalInput.value) || 0;
                const mLoss = parseFloat(mLossInput.value) || 0;
                mUsageSpan.textContent = Math.floor(mPrev + mArrival - mInventory - mLoss);
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
