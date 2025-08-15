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
    <div class="w-full max-w-2xl p-8 bg-white rounded-2xl shadow-xl space-y-6">
        <h1 class="text-3xl font-bold text-center text-gray-800">営業報告計算ツール</h1>
        
        <!-- 入力フォーム -->
        <div class="space-y-6">
            <!-- 営業指標入力フォーム -->
            <div class="space-y-4 border-b-2 pb-6">
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

            <!-- 支払い方法入力フォーム -->
            <div class="space-y-4 border-b-2 pb-6">
                <h2 class="text-xl font-bold text-gray-800">支払い方法</h2>
                <div>
                    <label for="cash" class="block text-sm font-medium text-gray-700">現金</label>
                    <input
                        type="number"
                        id="cash"
                        placeholder="例: 50000"
                        class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                    >
                </div>
                <div>
                    <label for="credit" class="block text-sm font-medium text-gray-700">クレジット</label>
                    <input
                        type="number"
                        id="credit"
                        placeholder="例: 30000"
                        class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                    >
                </div>
                <div>
                    <label for="eMoney" class="block text-sm font-medium text-gray-700">電子マネー</label>
                    <input
                        type="number"
                        id="eMoney"
                        placeholder="例: 15000"
                        class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2"
                    >
                </div>
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

            <!-- 在庫計算入力フォーム -->
            <div class="space-y-6 border-b-2 pb-6">
                <h2 class="text-xl font-bold text-gray-800">在庫計算</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Mパティ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Mパティ</h3>
                        <div>
                            <label for="mpCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="mpCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mpLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="mpLoose" placeholder="例: 10" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Zパティ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Zパティ</h3>
                        <div>
                            <label for="zpCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="zpCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zpLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="zpLoose" placeholder="例: 10" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Rパティ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Rパティ</h3>
                        <div>
                            <label for="rpCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="rpCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="rpLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="rpLoose" placeholder="例: 10" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Mバンズ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Mバンズ</h3>
                        <div>
                            <label for="mbCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="mbCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mbBag" class="block text-sm font-medium text-gray-700">袋数</label>
                            <input type="number" id="mbBag" placeholder="例: 2" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mbLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="mbLoose" placeholder="例: 3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Zバンズ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Zバンズ</h3>
                        <div>
                            <label for="zbCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="zbCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zbBag" class="block text-sm font-medium text-gray-700">袋数</label>
                            <input type="number" id="zbBag" placeholder="例: 2" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zbLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="zbLoose" placeholder="例: 3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- クープバンズ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">クープバンズ</h3>
                        <div>
                            <label for="qbBag" class="block text-sm font-medium text-gray-700">袋数</label>
                            <input type="number" id="qbBag" placeholder="例: 2" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="qbLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="qbLoose" placeholder="例: 3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- マフィンバンズ -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">マフィンバンズ</h3>
                        <div>
                            <label for="mCase" class="block text-sm font-medium text-gray-700">ケース数</label>
                            <input type="number" id="mCase" placeholder="例: 1" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mBag" class="block text-sm font-medium text-gray-700">袋数</label>
                            <input type="number" id="mBag" placeholder="例: 2" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mLoose" class="block text-sm font-medium text-gray-700">バラ</label>
                            <input type="number" id="mLoose" placeholder="例: 3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                </div>
            </div>

            <!-- 管理指数入力フォーム -->
            <div class="space-y-6">
                <h2 class="text-xl font-bold text-gray-800">管理指数</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Mパティ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Mパティ</h3>
                        <div>
                            <label for="mpPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="mpPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mpArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="mpArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mpLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="mpLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Zパティ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Zパティ</h3>
                        <div>
                            <label for="zpPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="zpPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zpArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="zpArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zpLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="zpLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Rパティ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Rパティ</h3>
                        <div>
                            <label for="rpPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="rpPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="rpArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="rpArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="rpLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="rpLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Mバンズ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Mバンズ</h3>
                        <div>
                            <label for="mbPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="mbPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mbArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="mbArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mbLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="mbLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- Zバンズ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">Zバンズ</h3>
                        <div>
                            <label for="zbPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="zbPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zbArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="zbArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="zbLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="zbLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- クープバンズ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">クープバンズ</h3>
                        <div>
                            <label for="qbPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="qbPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="qbArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="qbArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="qbLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="qbLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                    <!-- マフィンバンズ管理 -->
                    <div class="bg-gray-50 p-4 rounded-lg space-y-2">
                        <h3 class="text-lg font-bold text-gray-800">マフィンバンズ</h3>
                        <div>
                            <label for="mPrev" class="block text-sm font-medium text-gray-700">前残</label>
                            <input type="number" id="mPrev" placeholder="例: 200" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mArrival" class="block text-sm font-medium text-gray-700">入荷</label>
                            <input type="number" id="mArrival" placeholder="例: 1000" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                        <div>
                            <label for="mLoss" class="block text-sm font-medium text-gray-700">ロス</label>
                            <input type="number" id="mLoss" placeholder="例: 5" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm p-2">
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 計算ボタン -->
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

        <!-- 結果表示エリア -->
        <div class="space-y-4 pt-4 border-t-2 border-gray-200">
            <h2 class="text-xl font-bold text-gray-800">計算結果</h2>
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
            
            <hr class="border-gray-300">

            <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                <span class="text-gray-700 font-medium">支払い小計（現金以外）:</span>
                <span id="subtotalPayment" class="text-xl font-bold text-indigo-600"></span>
            </div>

            <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                <span class="text-gray-700 font-medium">総売上:</span>
                <span id="totalSales" class="text-xl font-bold text-indigo-600"></span>
            </div>

            <hr class="border-gray-300">

            <!-- 在庫計算結果 -->
            <h3 class="text-lg font-bold text-gray-800 mt-4">在庫結果</h3>
            <div class="space-y-2">
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Mパティ在庫:</span>
                    <span id="mpInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Zパティ在庫:</span>
                    <span id="zpInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Rパティ在庫:</span>
                    <span id="rpInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Mバンズ在庫:</span>
                    <span id="mbInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Zバンズ在庫:</span>
                    <span id="zbInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">クープバンズ在庫:</span>
                    <span id="qbInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">マフィンバンズ在庫:</span>
                    <span id="mInventory" class="text-xl font-bold text-indigo-600"></span>
                </div>
            </div>

            <hr class="border-gray-300">

            <!-- 管理指数結果 -->
            <h3 class="text-lg font-bold text-gray-800 mt-4">管理指数結果</h3>
            <div class="space-y-2">
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Mパティ実使用量:</span>
                    <span id="mpUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Zパティ実使用量:</span>
                    <span id="zpUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Rパティ実使用量:</span>
                    <span id="rpUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Mバンズ実使用量:</span>
                    <span id="mbUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">Zバンズ実使用量:</span>
                    <span id="zbUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">クープバンズ実使用量:</span>
                    <span id="qbUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
                <div class="flex justify-between items-center bg-gray-50 p-4 rounded-lg">
                    <span class="text-gray-700 font-medium">マフィンバンズ実使用量:</span>
                    <span id="mUsage" class="text-xl font-bold text-indigo-600"></span>
                </div>
            </div>
        </div>
    </div>

    <script>
        // DOM要素を取得
        // 営業指標
        const netSalesInput = document.getElementById('netSales');
        const customersInput = document.getElementById('customers');
        const workHoursInput = document.getElementById('workHours');
        const averagePriceSpan = document.getElementById('averagePrice');
        const salesPerHourSpan = document.getElementById('salesPerHour');
        const customersPerHourSpan = document.getElementById('customersPerHour');

        // 支払い方法
        const cashInput = document.getElementById('cash');
        const creditInput = document.getElementById('credit');
        const eMoneyInput = document.getElementById('eMoney');
        const prepaymentInput = document.getElementById('prepayment');
        const subtotalPaymentSpan = document.getElementById('subtotalPayment');
        const totalSalesSpan = document.getElementById('totalSales');
        
        // 在庫計算
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
        const mpInventorySpan = document.getElementById('mpInventory');
        const zpInventorySpan = document.getElementById('zpInventory');
        const rpInventorySpan = document.getElementById('rpInventory');
        const mbInventorySpan = document.getElementById('mbInventory');
        const zbInventorySpan = document.getElementById('zbInventory');
        const qbInventorySpan = document.getElementById('qbInventory');
        const mInventorySpan = document.getElementById('mInventory');

        // 管理指数
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
        const mpUsageSpan = document.getElementById('mpUsage');
        const zpUsageSpan = document.getElementById('zpUsage');
        const rpUsageSpan = document.getElementById('rpUsage');
        const mbUsageSpan = document.getElementById('mbUsage');
        const zbUsageSpan = document.getElementById('zbUsage');
        const qbUsageSpan = document.getElementById('qbUsage');
        const mUsageSpan = document.getElementById('mUsage');

        const calculateButton = document.getElementById('calculateBtn');

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

            // 在庫計算の入力値を取得し、数値に変換
            const mpCase = parseFloat(mpCaseInput.value) || 0;
            const mpLoose = parseFloat(mpLooseInput.value) || 0;
            const zpCase = parseFloat(zpCaseInput.value) || 0;
            const zpLoose = parseFloat(zpLooseInput.value) || 0;
            const rpCase = parseFloat(rpCaseInput.value) || 0;
            const rpLoose = parseFloat(rpLooseInput.value) || 0;
            const mbCase = parseFloat(mbCaseInput.value) || 0;
            const mbBag = parseFloat(mbBagInput.value) || 0;
            const mbLoose = parseFloat(mbLooseInput.value) || 0;
            const zbCase = parseFloat(zbCaseInput.value) || 0;
            const zbBag = parseFloat(zbBagInput.value) || 0;
            const zbLoose = parseFloat(zbLooseInput.value) || 0;
            const qbBag = parseFloat(qbBagInput.value) || 0;
            const qbLoose = parseFloat(qbLooseInput.value) || 0;
            const mCase = parseFloat(mCaseInput.value) || 0;
            const mBag = parseFloat(mBagInput.value) || 0;
            const mLoose = parseFloat(mLooseInput.value) || 0;

            // 管理指数の入力値を取得し、数値に変換
            const mpPrev = parseFloat(mpPrevInput.value) || 0;
            const mpArrival = parseFloat(mpArrivalInput.value) || 0;
            const mpLoss = parseFloat(mpLossInput.value) || 0;
            const zpPrev = parseFloat(zpPrevInput.value) || 0;
            const zpArrival = parseFloat(zpArrivalInput.value) || 0;
            const zpLoss = parseFloat(zpLossInput.value) || 0;
            const rpPrev = parseFloat(rpPrevInput.value) || 0;
            const rpArrival = parseFloat(rpArrivalInput.value) || 0;
            const rpLoss = parseFloat(rpLossInput.value) || 0;
            const mbPrev = parseFloat(mbPrevInput.value) || 0;
            const mbArrival = parseFloat(mbArrivalInput.value) || 0;
            const mbLoss = parseFloat(mbLossInput.value) || 0;
            const zbPrev = parseFloat(zbPrevInput.value) || 0;
            const zbArrival = parseFloat(zbArrivalInput.value) || 0;
            const zbLoss = parseFloat(zbLossInput.value) || 0;
            const qbPrev = parseFloat(qbPrevInput.value) || 0;
            const qbArrival = parseFloat(qbArrivalInput.value) || 0;
            const qbLoss = parseFloat(qbLossInput.value) || 0;
            const mPrev = parseFloat(mPrevInput.value) || 0;
            const mArrival = parseFloat(mArrivalInput.value) || 0;
            const mLoss = parseFloat(mLossInput.value) || 0;

            // 客単価を計算 (小数点以下第2位まで)
            const calculatedAveragePrice = customers !== 0 ? (netSales / customers).toFixed(2) : "0";
            averagePriceSpan.textContent = calculatedAveragePrice;

            // 労時売り上げを計算 (小数点以下第2位まで)
            const calculatedSalesPerHour = workHours !== 0 ? (netSales / workHours).toFixed(2) : "0";
            salesPerHourSpan.textContent = calculatedSalesPerHour;

            // 人時接客数を計算 (小数点以下第2位まで)
            const calculatedCustomersPerHour = workHours !== 0 ? (customers / workHours).toFixed(2) : "0";
            customersPerHourSpan.textContent = calculatedCustomersPerHour;
            
            // 支払い小計を計算 (小数点以下切り捨て)
            const calculatedSubtotalPayment = Math.floor(credit + eMoney + prepayment);
            subtotalPaymentSpan.textContent = calculatedSubtotalPayment;
            
            // 総売上を計算 (小数点以下切り捨て)
            const calculatedTotalSales = Math.floor(cash + credit + eMoney + prepayment);
            totalSalesSpan.textContent = calculatedTotalSales;

            // 在庫を計算
            const mpInventory = (mpCase * 96 + mpLoose);
            mpInventorySpan.textContent = mpInventory;
            const zpInventory = (zpCase * 96 + zpLoose);
            zpInventorySpan.textContent = zpInventory;
            const rpInventory = (rpCase * 90 + rpLoose);
            rpInventorySpan.textContent = rpInventory;
            const mbInventory = (mbCase * 24 + mbBag * 6 + mbLoose);
            mbInventorySpan.textContent = mbInventory;
            const zbInventory = (zbCase * 24 + zbBag * 6 + zbLoose);
            zbInventorySpan.textContent = zbInventory;
            const qbInventory = (qbBag * 12 + qbLoose);
            qbInventorySpan.textContent = qbInventory;
            const mInventory = (mCase * 72 + mBag * 6 + mLoose);
            mInventorySpan.textContent = mInventory;

            // 実使用量を計算
            const mpUsage = mpPrev + mpArrival - mpInventory - mpLoss;
            mpUsageSpan.textContent = mpUsage;
            const zpUsage = zpPrev + zpArrival - zpInventory - zpLoss;
            zpUsageSpan.textContent = zpUsage;
            const rpUsage = rpPrev + rpArrival - rpInventory - rpLoss;
            rpUsageSpan.textContent = rpUsage;
            const mbUsage = mbPrev + mbArrival - mbInventory - mbLoss;
            mbUsageSpan.textContent = mbUsage;
            const zbUsage = zbPrev + zbArrival - zbInventory - zbLoss;
            zbUsageSpan.textContent = zbUsage;
            const qbUsage = qbPrev + qbArrival - qbInventory - qbLoss;
            qbUsageSpan.textContent = qbUsage;
            const mUsage = mPrev + mArrival - mInventory - mLoss;
            mUsageSpan.textContent = mUsage;
        };

        // ボタンにクリックイベントリスナーを追加
        calculateButton.addEventListener('click', calculateMetrics);
    </script>
</body>
</html>
