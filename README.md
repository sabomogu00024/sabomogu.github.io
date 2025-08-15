<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>営報計算ツール</title>
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
    <div class="w-full max-w-4xl p-8 bg-white rounded-2xl shadow-xl space-y-6">
        <h1 class="text-3xl font-bold text-center text-gray-800">営業報告計算ツール</h1>
        
        <!-- 営業指標と収入のセクションを横並びに配置 -->
        <div class="flex flex-col lg:flex-row gap-6">

            <!-- 営業指標の入力と出力をまとめたセクション -->
            <div class="flex-1 space-y-6">
                <!-- 営業指標入力フォーム -->
                <div class="p-6 bg-gray-50 rounded-lg border border-gray-200 space-y-4">
                    <h2 class="text-xl font-bold text-gray-800">営業指標</h2>
                    <div>
                        <label for="netSales" class="block text-sm font-medium text-gray-700">Net売り上げ</label>
                        <input
                            type="number"
                            id="netSales"
                            placeholder="例: 100000"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                    <hr class="border-gray-300">
                    <div>
                        <label for="customers" class="block text-sm font-medium text-gray-700">組数</label>
                        <input
                            type="number"
                            id="customers"
                            placeholder="例: 10"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                    <hr class="border-gray-300">
                    <div>
                        <label for="workHours" class="block text-sm font-medium text-gray-700">労働時間数</label>
                        <input
                            type="number"
                            id="workHours"
                            placeholder="例: 8"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                </div>

                <!-- 営業指標の結果表示エリア -->
                <div class="space-y-4 p-6 bg-gray-50 rounded-lg border border-gray-200">
                    <h2 class="text-xl font-bold text-gray-800">営業指標 結果</h2>
                    <div class="flex justify-between items-center">
                        <span class="text-gray-700 font-medium">客単価:</span>
                        <span id="averagePrice" class="text-xl font-bold text-indigo-600"></span>
                    </div>
                    <hr class="border-gray-300">
                    <div class="flex justify-between items-center">
                        <span class="text-gray-700 font-medium">労時売り上げ:</span>
                        <span id="salesPerHour" class="text-xl font-bold text-indigo-600"></span>
                    </div>
                    <hr class="border-gray-300">
                    <div class="flex justify-between items-center">
                        <span class="text-gray-700 font-medium">人時接客数:</span>
                        <span id="customersPerHour" class="text-xl font-bold text-indigo-600"></span>
                    </div>
                </div>
            </div>

            <!-- 収入の入力と出力をまとめたセクション -->
            <div class="flex-1 space-y-6">
                <!-- 収入入力フォーム -->
                <div class="p-6 bg-gray-50 rounded-lg border border-gray-200 space-y-4">
                    <h2 class="text-xl font-bold text-gray-800">収入</h2>
                    <div>
                        <label for="cash" class="block text-sm font-medium text-gray-700">現金</label>
                        <input
                            type="number"
                            id="cash"
                            placeholder="例: 50000"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                    <hr class="border-gray-300">
                    <div>
                        <label for="credit" class="block text-sm font-medium text-gray-700">クレジット</label>
                        <input
                            type="number"
                            id="credit"
                            placeholder="例: 30000"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                    <hr class="border-gray-300">
                    <div>
                        <label for="eMoney" class="block text-sm font-medium text-gray-700">電子マネー</label>
                        <input
                            type="number"
                            id="eMoney"
                            placeholder="例: 15000"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                    <hr class="border-gray-300">
                    <div>
                        <label for="prepayment" class="block text-sm font-medium text-gray-700">事前会計</label>
                        <input
                            type="number"
                            id="prepayment"
                            placeholder="例: 5000"
                            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                        >
                    </div>
                </div>

                <!-- 収入の結果表示エリア -->
                <div class="space-y-4 p-6 bg-gray-50 rounded-lg border border-gray-200">
                    <h2 class="text-xl font-bold text-gray-800">収入 結果</h2>
                    <div class="flex justify-between items-center">
                        <span class="text-gray-700 font-medium">支払い小計（現金以外）:</span>
                        <span id="subtotalPayment" class="text-xl font-bold text-indigo-600"></span>
                    </div>
                    <hr class="border-gray-300">
                    <div class="flex justify-between items-center">
                        <span class="text-gray-700 font-medium">総売上:</span>
                        <span id="totalSales" class="text-xl font-bold text-indigo-600"></span>
                    </div>
                </div>
            </div>
        </div>

        <button
            id="calculateBtn"
            class="w-full inline-flex justify-center items-center px-6 py-3 border border-transparent shadow-sm text-base font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-200"
        >
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="h-5 w-5 mr-2"
            >
                <polygon points="5 3 19 12 5 21 5 3"></polygon>
            </svg>
            計算
        </button>
    </div>

    <script>
        // DOM要素を取得
        const netSalesInput = document.getElementById('netSales');
        const customersInput = document.getElementById('customers');
        const workHoursInput = document.getElementById('workHours');
        const cashInput = document.getElementById('cash');
        const creditInput = document.getElementById('credit');
        const eMoneyInput = document.getElementById('eMoney');
        const prepaymentInput = document.getElementById('prepayment');
        const calculateButton = document.getElementById('calculateBtn');
        const averagePriceSpan = document.getElementById('averagePrice');
        const salesPerHourSpan = document.getElementById('salesPerHour');
        const customersPerHourSpan = document.getElementById('customersPerHour');
        const subtotalPaymentSpan = document.getElementById('subtotalPayment');
        const totalSalesSpan = document.getElementById('totalSales');

        // 計算を実行する関数
        const calculateMetrics = () => {
            // 営業指標の入力値を取得し、数値に変換
            const netSales = parseFloat(netSalesInput.value) || 0;
            const customers = parseFloat(customersInput.value) || 0;
            const workHours = parseFloat(workHoursInput.value) || 0;

            // 支払い方法の入力値を取得し、数値に変換
            const cash = parseFloat(cashInput.value) || 0;
            const credit = parseFloat(creditInput.value) || 0;
            const eMoney = parseFloat(eMoneyInput.value) || 0;
            const prepayment = parseFloat(prepaymentInput.value) || 0;

            // 客単価を計算
            const calculatedAveragePrice = customers !== 0 ? (netSales / customers).toFixed(2) : "0";
            averagePriceSpan.textContent = calculatedAveragePrice;

            // 労時売り上げを計算
            const calculatedSalesPerHour = workHours !== 0 ? (netSales / workHours).toFixed(2) : "0";
            salesPerHourSpan.textContent = calculatedSalesPerHour;

            // 人時接客数を計算
            const calculatedCustomersPerHour = workHours !== 0 ? (customers / workHours).toFixed(2) : "0";
            customersPerHourSpan.textContent = calculatedCustomersPerHour;
            
            // 支払い小計を計算
            const calculatedSubtotalPayment = (credit + eMoney + prepayment).toFixed(2);
            subtotalPaymentSpan.textContent = calculatedSubtotalPayment;
            
            // 総売上を計算
            const calculatedTotalSales = (cash + credit + eMoney + prepayment).toFixed(2);
            totalSalesSpan.textContent = calculatedTotalSales;
        };

        // ボタンにクリックイベントリスナーを追加
        calculateButton.addEventListener('click', calculateMetrics);
    </script>
</body>
</html>
