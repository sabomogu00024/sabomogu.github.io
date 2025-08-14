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
    <div class="w-full max-w-lg p-8 bg-white rounded-2xl shadow-xl space-y-6">
        <h1 class="text-3xl font-bold text-center text-gray-800">営報計算ツール</h1>
        
        <div class="space-y-4">
            <div>
                <label for="netSales" class="block text-sm font-medium text-gray-700">Net売り上げ</label>
                <input
                    type="number"
                    id="netSales"
                    placeholder="例: 100000"
                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                >
            </div>

            <div>
                <label for="customers" class="block text-sm font-medium text-gray-700">組数</label>
                <input
                    type="number"
                    id="customers"
                    placeholder="例: 10"
                    class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                >
            </div>

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

        <div class="space-y-4 pt-4 border-t-2 border-gray-200">
            <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                <span class="text-gray-700 font-medium">客単価:</span>
                <span id="averagePrice" class="text-xl font-bold text-indigo-600"></span>
            </div>

            <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                <span class="text-gray-700 font-medium">労時売り上げ:</span>
                <span id="salesPerHour" class="text-xl font-bold text-indigo-600"></span>
            </div>

            <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                <span class="text-gray-700 font-medium">人時接客数:</span>
                <span id="customersPerHour" class="text-xl font-bold text-indigo-600"></span>
            </div>
        </div>
    </div>

    <script>
        // DOM要素を取得
        const netSalesInput = document.getElementById('netSales');
        const customersInput = document.getElementById('customers');
        const workHoursInput = document.getElementById('workHours');
        const calculateButton = document.getElementById('calculateBtn');
        const averagePriceSpan = document.getElementById('averagePrice');
        const salesPerHourSpan = document.getElementById('salesPerHour');
        const customersPerHourSpan = document.getElementById('customersPerHour');

        // 計算を実行する関数
        const calculateMetrics = () => {
            // 入力値を取得し、数値に変換
            const netSales = parseFloat(netSalesInput.value);
            const customers = parseFloat(customersInput.value);
            const workHours = parseFloat(workHoursInput.value);
            
            // エラーハンドリング
            if (isNaN(netSales) || isNaN(customers) || isNaN(workHours)) {
                alert("エラー: 有効な数値を入力してください。");
                return;
            }

            // 客単価を計算
            const calculatedAveragePrice = customers !== 0 ? (netSales / customers).toFixed(2) : "0では割り算できません";
            averagePriceSpan.textContent = calculatedAveragePrice;

            // 労時売り上げを計算
            const calculatedSalesPerHour = workHours !== 0 ? (netSales / workHours).toFixed(2) : "0では割り算できません";
            salesPerHourSpan.textContent = calculatedSalesPerHour;

            // 人時接客数を計算
            const calculatedCustomersPerHour = workHours !== 0 ? (customers / workHours).toFixed(2) : "0では割り算できません";
            customersPerHourSpan.textContent = calculatedCustomersPerHour;
        };

        // ボタンにクリックイベントリスナーを追加
        calculateButton.addEventListener('click', calculateMetrics);
    </script>
</body>
</html>
