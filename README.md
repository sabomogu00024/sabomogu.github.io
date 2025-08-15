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
        .input-group {
            @apply flex flex-col space-y-2;
        }
        .input-label {
            @apply text-sm font-medium text-gray-700;
        }
        .input-field {
            @apply mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2;
        }
        .result-box {
            @apply bg-white p-4 rounded-lg shadow-sm;
        }
        .result-label {
            @apply text-sm font-medium text-gray-500;
        }
        .result-value {
            @apply text-lg font-bold text-gray-800;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">
    <div class="w-full max-w-2xl p-8 bg-white rounded-2xl shadow-xl space-y-6">
        <h1 class="text-3xl font-bold text-center text-gray-800">営業指標計算ツール</h1>

        <!-- 営業指標セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700">営業指標</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="input-group">
                    <label for="netSales" class="input-label">Net売り上げ</label>
                    <input type="number" id="netSales" placeholder="例: 100000" class="input-field">
                </div>
                <div class="input-group">
                    <label for="customers" class="input-label">組数</label>
                    <input type="number" id="customers" placeholder="例: 50" class="input-field">
                </div>
                <div class="input-group">
                    <label for="workHours" class="input-label">労働時間数</label>
                    <input type="number" id="workHours" placeholder="例: 8" class="input-field">
                </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-4">
                <div class="result-box">
                    <p class="result-label">客単価</p>
                    <p id="averagePrice" class="result-value">-</p>
                </div>
                <div class="result-box">
                    <p class="result-label">労時売り上げ</p>
                    <p id="salesPerHour" class="result-value">-</p>
                </div>
                <div class="result-box">
                    <p class="result-label">人時接客数</p>
                    <p id="customersPerHour" class="result-value">-</p>
                </div>
            </div>
        </div>

        <!-- 支払い方法セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700">支払い方法</h2>
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                <div class="input-group">
                    <label for="cash" class="input-label">現金</label>
                    <input type="number" id="cash" class="input-field">
                </div>
                <div class="input-group">
                    <label for="credit" class="input-label">クレジット</label>
                    <input type="number" id="credit" class="input-field">
                </div>
                <div class="input-group">
                    <label for="eMoney" class="input-label">電子マネー</label>
                    <input type="number" id="eMoney" class="input-field">
                </div>
                <div class="input-group">
                    <label for="prepayment" class="input-label">事前会計</label>
                    <input type="number" id="prepayment" class="input-field">
                </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
                <div class="result-box">
                    <p class="result-label">支払い小計</p>
                    <p id="subtotalPayment" class="result-value">-</p>
                </div>
                <div class="result-box">
                    <p class="result-label">総売上</p>
                    <p id="totalSales" class="result-value">-</p>
                </div>
            </div>
        </div>

        <!-- 在庫セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700">在庫計算</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Mパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Mパティ</h3>
                    <label class="input-label">ケース数: <input type="number" id="mpCase" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="mpLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="mpInventory" class="result-value">-</p>
                </div>
                <!-- Zパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Zパティ</h3>
                    <label class="input-label">ケース数: <input type="number" id="zpCase" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="zpLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="zpInventory" class="result-value">-</p>
                </div>
                <!-- Rパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Rパティ</h3>
                    <label class="input-label">ケース数: <input type="number" id="rpCase" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="rpLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="rpInventory" class="result-value">-</p>
                </div>
                <!-- Mバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Mバンズ</h3>
                    <label class="input-label">ケース数: <input type="number" id="mbCase" class="input-field"></label>
                    <label class="input-label">袋数: <input type="number" id="mbBag" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="mbLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="mbInventory" class="result-value">-</p>
                </div>
                <!-- Zバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Zバンズ</h3>
                    <label class="input-label">ケース数: <input type="number" id="zbCase" class="input-field"></label>
                    <label class="input-label">袋数: <input type="number" id="zbBag" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="zbLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="zbInventory" class="result-value">-</p>
                </div>
                <!-- クープバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">クープバンズ</h3>
                    <label class="input-label">袋数: <input type="number" id="qbBag" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="qbLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="qbInventory" class="result-value">-</p>
                </div>
                <!-- マフィンバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">マフィンバンズ</h3>
                    <label class="input-label">ケース数: <input type="number" id="mCase" class="input-field"></label>
                    <label class="input-label">袋数: <input type="number" id="mBag" class="input-field"></label>
                    <label class="input-label">バラ: <input type="number" id="mLoose" class="input-field"></label>
                    <p class="result-label mt-2">在庫:</p>
                    <p id="mInventory" class="result-value">-</p>
                </div>
            </div>
        </div>

        <!-- 管理指数セクション -->
        <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-700">管理指数</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Mパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Mパティ</h3>
                    <label class="input-label">前残: <input type="number" id="mpPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="mpArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="mpLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="mpUsage" class="result-value">-</p>
                </div>
                <!-- Zパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Zパティ</h3>
                    <label class="input-label">前残: <input type="number" id="zpPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="zpArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="zpLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="zpUsage" class="result-value">-</p>
                </div>
                <!-- Rパティ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Rパティ</h3>
                    <label class="input-label">前残: <input type="number" id="rpPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="rpArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="rpLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="rpUsage" class="result-value">-</p>
                </div>
                <!-- Mバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Mバンズ</h3>
                    <label class="input-label">前残: <input type="number" id="mbPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="mbArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="mbLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="mbUsage" class="result-value">-</p>
                </div>
                <!-- Zバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">Zバンズ</h3>
                    <label class="input-label">前残: <input type="number" id="zbPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="zbArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="zbLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="zbUsage" class="result-value">-</p>
                </div>
                <!-- クープバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">クープバンズ</h3>
                    <label class="input-label">前残: <input type="number" id="qbPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="qbArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="qbLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="qbUsage" class="result-value">-</p>
                </div>
                <!-- マフィンバンズ -->
                <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                    <h3 class="text-lg font-medium text-gray-700">マフィンバンズ</h3>
                    <label class="input-label">前残: <input type="number" id="mPrev" class="input-field"></label>
                    <label class="input-label">入荷: <input type="number" id="mArrival" class="input-field"></label>
                    <label class="input-label">ロス: <input type="number" id="mLoss" class="input-field"></label>
                    <p class="result-label mt-2">実使用量:</p>
                    <p id="mUsage" class="result-value">-</p>
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
            const mpInventorySpan = document.getElementById('mpInventory');
            const zpInventorySpan = document.getElementById('zpInventory');
            const rpInventorySpan = document.getElementById('rpInventory');
            const mbInventorySpan = document.getElementById('mbInventory');
            const zbInventorySpan = document.getElementById('zbInventory');
            const qbInventorySpan = document.getElementById('qbInventory');
            const mInventorySpan = document.getElementById('mInventory');
            const mpUsageSpan = document.getElementById('mpUsage');
            const zpUsageSpan = document.getElementById('zpUsage');
            const rpUsageSpan = document.getElementById('rpUsage');
            const mbUsageSpan = document.getElementById('mbUsage');
            const zbUsageSpan = document.getElementById('zbUsage');
            const qbUsageSpan = document.getElementById('qbUsage');
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
            const zpCaseInput = document.getElementById('zpCase');
            const zpLooseInput = document.getElementById('zpLoose');
            const rpCaseInput = document.getElementById('rpCase');
            const rpLooseInput = document.getElementById('rpLoose');
            const mbCaseInput = document.getElementById('mbCase');
            const mbBagInput = document.getElementById('mbBag');
            const mbLooseInput = document.getElementById('mbLoose');
            const zbCaseInput = document.getElementById('zbCase');
            const zbBagInput = document.getElementById('zbBag');
            const zbLooseInput = document.getElementById('zbLoose');
            const qbBagInput = document.getElementById('qbBag');
            const qbLooseInput = document.getElementById('qbLoose');
            const mCaseInput = document.getElementById('mCase');
            const mBagInput = document.getElementById('mBag');
            const mLooseInput = document.getElementById('mLoose');
            const mpPrevInput = document.getElementById('mpPrev');
            const mpArrivalInput = document.getElementById('mpArrival');
            const mpLossInput = document.getElementById('mpLoss');
            const zpPrevInput = document.getElementById('zpPrev');
            const zpArrivalInput = document.getElementById('zpArrival');
            const zpLossInput = document.getElementById('zpLoss');
            const rpPrevInput = document.getElementById('rpPrev');
            const rpArrivalInput = document.getElementById('rpArrival');
            const rpLossInput = document.getElementById('rpLoss');
            const mbPrevInput = document.getElementById('mbPrev');
            const mbArrivalInput = document.getElementById('mbArrival');
            const mbLossInput = document.getElementById('mbLoss');
            const zbPrevInput = document.getElementById('zbPrev');
            const zbArrivalInput = document.getElementById('zbArrival');
            const zbLossInput = document.getElementById('zbLoss');
            const qbPrevInput = document.getElementById('qbPrev');
            const qbArrivalInput = document.getElementById('qbArrival');
            const qbLossInput = document.getElementById('qbLoss');
            const mPrevInput = document.getElementById('mPrev');
            const mArrivalInput = document.getElementById('mArrival');
            const mLossInput = document.getElementById('mLoss');

            // 全ての入力フィールドを配列にまとめる
            const allInputs = [
                netSalesInput, customersInput, workHoursInput,
                cashInput, creditInput, eMoneyInput, prepaymentInput,
                mpCaseInput, mpLooseInput, zpCaseInput, zpLooseInput,
                rpCaseInput, rpLooseInput, mbCaseInput, mbBagInput,
                mbLooseInput, zbCaseInput, zbBagInput, zbLooseInput,
                qbBagInput, qbLooseInput, mCaseInput, mBagInput, mLooseInput,
                mpPrevInput, mpArrivalInput, mpLossInput, zpPrevInput,
                zpArrivalInput, zpLossInput, rpPrevInput, rpArrivalInput,
                rpLossInput, mbPrevInput, mbArrivalInput, mbLossInput,
                zbPrevInput, zbArrivalInput, zbLossInput, qbPrevInput,
                qbArrivalInput, qbLossInput, mPrevInput, mArrivalInput, mLossInput
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

                subtotalPaymentSpan.textContent = (credit + eMoney + prepayment).toFixed(2);
                totalSalesSpan.textContent = (cash + credit + eMoney + prepayment).toFixed(2);

                // 在庫計算
                const mpCase = parseFloat(mpCaseInput.value) || 0;
                const mpLoose = parseFloat(mpLooseInput.value) || 0;
                const mpInventory = mpCase * 96 + mpLoose;
                mpInventorySpan.textContent = mpInventory;

                const zpCase = parseFloat(zpCaseInput.value) || 0;
                const zpLoose = parseFloat(zpLooseInput.value) || 0;
                const zpInventory = zpCase * 64 + zpLoose;
                zpInventorySpan.textContent = zpInventory;

                const rpCase = parseFloat(rpCaseInput.value) || 0;
                const rpLoose = parseFloat(rpLooseInput.value) || 0;
                const rpInventory = rpCase * 90 + rpLoose;
                rpInventorySpan.textContent = rpInventory;
                
                const mbCase = parseFloat(mbCaseInput.value) || 0;
                const mbBag = parseFloat(mbBagInput.value) || 0;
                const mbLoose = parseFloat(mbLooseInput.value) || 0;
                const mbInventory = mbCase * 24 + mbBag * 6 + mbLoose;
                mbInventorySpan.textContent = mbInventory;
                
                const zbCase = parseFloat(zbCaseInput.value) || 0;
                const zbBag = parseFloat(zbBagInput.value) || 0;
                const zbLoose = parseFloat(zbLooseInput.value) || 0;
                const zbInventory = zbCase * 24 + zbBag * 6 + zbLoose;
                zbInventorySpan.textContent = zbInventory;
                
                const qbBag = parseFloat(qbBagInput.value) || 0;
                const qbLoose = parseFloat(qbLooseInput.value) || 0;
                const qbInventory = qbBag * 12 + qbLoose;
                qbInventorySpan.textContent = qbInventory;
                
                const mCase = parseFloat(mCaseInput.value) || 0;
                const mBag = parseFloat(mBagInput.value) || 0;
                const mLoose = parseFloat(mLooseInput.value) || 0;
                const mInventory = mCase * 72 + mBag * 6 + mLoose;
                mInventorySpan.textContent = mInventory;

                // 管理指数
                const mpPrev = parseFloat(mpPrevInput.value) || 0;
                const mpArrival = parseFloat(mpArrivalInput.value) || 0;
                const mpLoss = parseFloat(mpLossInput.value) || 0;
                mpUsageSpan.textContent = (mpPrev + mpArrival - mpInventory - mpLoss).toFixed(2);

                const zpPrev = parseFloat(zpPrevInput.value) || 0;
                const zpArrival = parseFloat(zpArrivalInput.value) || 0;
                const zpLoss = parseFloat(zpLossInput.value) || 0;
                zpUsageSpan.textContent = (zpPrev + zpArrival - zpInventory - zpLoss).toFixed(2);
                
                const rpPrev = parseFloat(rpPrevInput.value) || 0;
                const rpArrival = parseFloat(rpArrivalInput.value) || 0;
                const rpLoss = parseFloat(rpLossInput.value) || 0;
                rpUsageSpan.textContent = (rpPrev + rpArrival - rpInventory - rpLoss).toFixed(2);

                const mbPrev = parseFloat(mbPrevInput.value) || 0;
                const mbArrival = parseFloat(mbArrivalInput.value) || 0;
                const mbLoss = parseFloat(mbLossInput.value) || 0;
                mbUsageSpan.textContent = (mbPrev + mbArrival - mbInventory - mbLoss).toFixed(2);
                
                const zbPrev = parseFloat(zbPrevInput.value) || 0;
                const zbArrival = parseFloat(zbArrivalInput.value) || 0;
                const zbLoss = parseFloat(zbLossInput.value) || 0;
                zbUsageSpan.textContent = (zbPrev + zbArrival - zbInventory - zbLoss).toFixed(2);
                
                const qbPrev = parseFloat(qbPrevInput.value) || 0;
                const qbArrival = parseFloat(qbArrivalInput.value) || 0;
                const qbLoss = parseFloat(qbLossInput.value) || 0;
                qbUsageSpan.textContent = (qbPrev + qbArrival - qbInventory - qbLoss).toFixed(2);
                
                const mPrev = parseFloat(mPrevInput.value) || 0;
                const mArrival = parseFloat(mArrivalInput.value) || 0;
                const mLoss = parseFloat(mLossInput.value) || 0;
                mUsageSpan.textContent = (mPrev + mArrival - mInventory - mLoss).toFixed(2);
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
