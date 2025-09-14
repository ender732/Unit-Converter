<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Unit Converter</title>
    <!-- Use Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom CSS to ensure the UI is centered and looks good */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f3f4f6;
            padding: 1rem;
        }
    </style>
</head>
<body class="bg-gray-100">

    <div class="max-w-md w-full p-8 bg-white rounded-xl shadow-2xl space-y-6 transform transition-all duration-300 hover:scale-105">
        <h1 class="text-3xl font-bold text-center text-gray-800">Unit Converter</h1>
        <p class="text-center text-gray-600">Convert between Kilometers and Miles</p>

        <!-- Input and Select fields -->
        <div class="space-y-4">
            <div>
                <label for="inputValue" class="block text-sm font-medium text-gray-700 mb-1">Value to convert</label>
                <input type="number" id="inputValue" placeholder="Enter a number"
                       class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all duration-200">
            </div>

            <div>
                <label for="conversionType" class="block text-sm font-medium text-gray-700 mb-1">Conversion Direction</label>
                <select id="conversionType"
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all duration-200 bg-white">
                    <option value="kmToMi">Kilometers to Miles</option>
                    <option value="miToKm">Miles to Kilometers</option>
                </select>
            </div>
        </div>

        <!-- Conversion Button -->
        <div class="pt-4">
            <button id="convertBtn"
                    class="w-full py-3 bg-blue-600 text-white font-semibold rounded-lg shadow-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 transition-all duration-200 transform hover:scale-105">
                Convert
            </button>
        </div>

        <!-- Output Display -->
        <div id="resultContainer" class="p-4 bg-gray-50 rounded-lg text-center border border-gray-200">
            <p id="resultText" class="text-xl font-medium text-gray-800">Result will be displayed here.</p>
        </div>
    </div>

    <!-- JavaScript for logic -->
    <script>
        window.onload = function() {
            // Get references to all necessary DOM elements
            const inputValueEl = document.getElementById('inputValue');
            const conversionTypeEl = document.getElementById('conversionType');
            const convertBtn = document.getElementById('convertBtn');
            const resultTextEl = document.getElementById('resultText');

            // Add event listener to the convert button
            convertBtn.addEventListener('click', convertUnits);

            // Function to perform the conversion
            function convertUnits() {
                // Get the user's input value
                const value = parseFloat(inputValueEl.value);

                // Check if the input is a valid number
                if (isNaN(value)) {
                    resultTextEl.textContent = "Please enter a valid number.";
                    resultTextEl.classList.add('text-red-500'); // Add a red color for errors
                    return; // Exit the function
                } else {
                    resultTextEl.classList.remove('text-red-500'); // Remove red color if valid
                }

                // Get the selected conversion type
                const type = conversionTypeEl.value;
                let result;

                // Perform the conversion based on the selected type
                if (type === 'kmToMi') {
                    // Convert kilometers to miles (1 km = 0.621371 miles)
                    result = value * 0.621371;
                    resultTextEl.textContent = `${value} km is approximately ${result.toFixed(2)} mi.`;
                } else if (type === 'miToKm') {
                    // Convert miles to kilometers (1 mi = 1.60934 km)
                    result = value * 1.60934;
                    resultTextEl.textContent = `${value} mi is approximately ${result.toFixed(2)} km.`;
                }
            }
        };
    </script>
</body>
</html>
