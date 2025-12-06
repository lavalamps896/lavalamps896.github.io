

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hennig Financial LLC | Interactive Service Explorer</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- Chosen Palette: Warm Professional -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        stone: { 50: '#fafaf9', 100: '#f5f5f4', 200: '#e7e5e4', 800: '#292524', 900: '#1c1917' },
                        navy: { 800: '#1e3a8a', 900: '#172554' },
                        forest: { 600: '#059669', 700: '#047857' },
                        alert: { 500: '#f97316' }
                    },
                    fontFamily: { sans: ['Inter', 'system-ui', 'sans-serif'] }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        .chart-container { position: relative; width: 100%; max-width: 500px; margin: 0 auto; height: 300px; max-height: 300px; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #ccc; border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: #999; }
        .tab-active { border-bottom: 3px solid #1e3a8a; color: #1e3a8a; font-weight: 600; }
        .service-card { transition: all 0.2s ease-in-out; }
        .service-card:hover { transform: translateY(-2px); box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1); }
    </style>
</head>
<body class="bg-stone-50 text-stone-800">

    <!-- Navigation -->
    <header class="bg-navy-900 text-stone-50 shadow-md">
        <div class="container mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center">
            <div>
                <h1 class="text-2xl font-bold tracking-tight">Hennig Financial LLC</h1>
                <p class="text-sm text-stone-300">Proactive Accounting: Compliance & Audit-Ready Support</p>
            </div>
            <div class="mt-4 md:mt-0 flex gap-4 text-sm">
                <button onclick="scrollToSection('services')" class="hover:text-forest-400 transition">Services</button>
                <button onclick="scrollToSection('about')" class="hover:text-forest-400 transition">About Ron</button>
                <button onclick="scrollToSection('contact')" class="bg-forest-600 hover:bg-forest-700 px-4 py-2 rounded font-semibold transition">Book Consultation</button>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="container mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-8">

        <!-- Intro -->
        <section class="lg:col-span-12 mb-4 bg-white p-6 rounded-lg shadow-sm border-l-4 border-navy-800">
            <h2 class="text-xl font-bold text-navy-800 mb-2">Beyond Bookkeeping: Audit-Ready Financials</h2>
            <p class="text-stone-600 mb-4">
                Welcome! I provide a comprehensive suite of financial services designed to reduce risk and increase confidence. 
                Whether you're a freelancer, a small business owner, or a non-profit, my goal is to provide **transparent pricing** and **defensible records**.
            </p>
            <div class="flex flex-wrap gap-2">
                <span class="px-3 py-1 bg-stone-100 text-stone-600 text-xs rounded-full font-semibold">Individuals & Families</span>
                <span class="px-3 py-1 bg-stone-100 text-stone-600 text-xs rounded-full font-semibold">LGBTQ+ Community</span>
                <span class="px-3 py-1 bg-stone-100 text-stone-600 text-xs rounded-full font-semibold">Freelancers</span>
                <span class="px-3 py-1 bg-stone-100 text-stone-600 text-xs rounded-full font-semibold">Small Businesses</span>
            </div>
        </section>

        <!-- Left Column: Navigation -->
        <aside class="lg:col-span-2 lg:block" id="services">
            <div class="bg-white rounded-lg shadow-sm p-4 sticky top-4">
                <h3 class="text-xs font-bold text-stone-400 uppercase tracking-wider mb-4">Explore Services</h3>
                <nav class="flex flex-row lg:flex-col gap-2 overflow-x-auto lg:overflow-visible pb-2 lg:pb-0">
                    <button onclick="switchTab('tax')" id="btn-tax" class="tab-btn text-left px-4 py-2 rounded-md hover:bg-stone-50 text-sm font-medium transition whitespace-nowrap tab-active">Tax Preparation</button>
                    <button onclick="switchTab('bookkeeping')" id="btn-bookkeeping" class="tab-btn text-left px-4 py-2 rounded-md hover:bg-stone-50 text-sm font-medium transition whitespace-nowrap">Bookkeeping</button>
                    <button onclick="switchTab('payroll')" id="btn-payroll" class="tab-btn text-left px-4 py-2 rounded-md hover:bg-stone-50 text-sm font-medium transition whitespace-nowrap">Payroll</button>
                    <button onclick="switchTab('advisory')" id="btn-advisory" class="tab-btn text-left px-4 py-2 rounded-md hover:bg-stone-50 text-sm font-medium transition whitespace-nowrap">HR & Recruiting</button>
                    <button onclick="switchTab('consulting')" id="btn-consulting" class="tab-btn text-left px-4 py-2 rounded-md hover:bg-stone-50 text-sm font-medium transition whitespace-nowrap">Consulting & Formation</button>
                </nav>
            </div>
        </aside>

        <!-- Center Column: Dynamic Content -->
        <section class="lg:col-span-6 space-y-6 min-h-[600px]">
            <div id="content-area">
                <!-- Content injected via JS -->
            </div>
        </section>

        <!-- Right Column: Quote Estimator -->
        <aside class="lg:col-span-4">
            <div class="bg-navy-900 text-stone-100 rounded-lg shadow-lg p-6 sticky top-4">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-lg font-bold">Your Estimate</h3>
                    <button onclick="resetQuote()" class="text-xs text-stone-400 hover:text-white underline">Reset</button>
                </div>

                <div class="mb-6">
                    <label class="block text-xs text-stone-400 mb-1">Have a discount code?</label>
                    <div class="flex gap-2">
                        <input type="text" id="discount-input" placeholder="Enter code" class="flex-grow bg-navy-800 border border-navy-700 text-stone-100 text-sm rounded px-3 py-2 focus:outline-none focus:border-forest-600 uppercase">
                        <button onclick="applyDiscountCode()" class="bg-forest-600 hover:bg-forest-700 text-white text-xs font-bold px-3 py-2 rounded transition">Apply</button>
                        <button onclick="clearDiscountCode()" class="bg-stone-600 hover:bg-stone-700 text-white text-xs font-bold px-3 py-2 rounded transition">&times;</button>
                    </div>
                    <p id="discount-feedback" class="text-xs mt-1 h-4"></p>
                </div>

                <div id="selected-items" class="space-y-2 mb-6 max-h-60 overflow-y-auto pr-2 text-sm">
                    <p class="text-stone-500 italic text-center py-4">Select services to build your quote.</p>
                </div>

                <div class="border-t border-navy-700 pt-4 space-y-2">
                    <div class="flex justify-between items-center">
                        <span class="text-stone-300">One-Time / Annual</span>
                        <span id="total-onetime" class="font-bold text-xl">$0</span>
                    </div>
                    <div class="flex justify-between items-center">
                        <span class="text-stone-300">Monthly Recurring</span>
                        <span id="total-monthly" class="font-bold text-xl">$0</span>
                    </div>
                </div>

                <div class="mt-6 pt-6 border-t border-navy-700">
                    <h4 class="text-xs font-bold text-stone-400 mb-2 uppercase text-center">Cost Composition</h4>
                    <div class="chart-container" style="height: 180px;">
                        <canvas id="quoteChart"></canvas>
                    </div>
                </div>

                <div class="mt-6">
                    <button onclick="alert('In a real app, this would email your quote!')" class="w-full bg-forest-600 hover:bg-forest-700 text-white font-bold py-3 rounded transition shadow-md">
                        Request This Package
                    </button>
                </div>
            </div>
        </aside>

    </main>

    <!-- About / Footer -->
    <section id="about" class="bg-white border-t border-stone-200 py-12">
        <div class="container mx-auto px-4 max-w-4xl text-center">
            <h2 class="text-2xl font-bold text-navy-900 mb-4">Meet Ron</h2>
            <div class="w-24 h-1 bg-forest-600 mx-auto mb-6"></div>
            <p class="text-lg text-stone-600 mb-8">
                I'm an auditor in public accounting with deep experience in commercial & real estate audits and financial analysis. 
                I didn't just learn tax from software; I learned it by conducting compliance audits. 
                I founded Hennig Financial to offer affordable, transparent support for real people.
            </p>
        </div>
    </section>

    <footer id="contact" class="bg-navy-900 text-stone-400 py-8">
        <div class="container mx-auto px-4 text-center">
            <h3 class="text-white font-bold text-lg mb-2">Hennig Financial LLC</h3>
            <p class="text-xs">&copy; 2025 Hennig Financial LLC. All rights reserved.</p>
        </div>
    </footer>

    <!-- Logic -->
    <script>
        // --- CONSTANTS & DATA ---
        
        const servicesData = {
            advisory: {
                title: "HR & Recruiting Services",
                intro: "Professional HR support, recruiting, and onboarding for small businesses.",
                items: [
                    { id: 'h1', name: "Job Description Creation", price: 125, type: 'onetime', cat: 'advisory', desc: "Professional job description with compensation analysis." },
                    { id: 'h2', name: "Salary Benchmarking", price: 175, type: 'onetime', cat: 'advisory', desc: "Market research & competitor benchmarks." },
                    { id: 'h3', name: "Candidate Screening", price: 150, type: 'onetime', cat: 'advisory', desc: "Resume review + phone screen + summary per candidate." },
                    { id: 'h4', name: "Interview Support", price: 300, type: 'onetime', cat: 'advisory', desc: "Screening + structured interview + scorecard per candidate." },
                    { id: 'h5', name: "Hiring Support Package", price: 500, type: 'onetime', cat: 'advisory', desc: "Full cycle support per role." },
                    { id: 'h6', name: "New Hire Onboarding", price: 200, type: 'onetime', cat: 'advisory', desc: "I-9, W-4, payroll setup & first-week plan per hire." },
                    { id: 'h7', name: "Employee Handbook", price: 400, type: 'onetime', cat: 'advisory', desc: "Custom small-business handbook creation." },
                    { id: 'h8', name: "HR Advisory Retainer", price: 75, type: 'monthly', cat: 'advisory', desc: "Ongoing monthly support (Est. $50-$100/mo)." }
                ]
            },
            consulting: {
                title: "Consulting & Formation",
                intro: "Expert guidance on business structure, risk, and strategy.",
                items: [
                    { id: 'a1', name: "Internal Controls Review", price: 1199, type: 'onetime', cat: 'consulting', desc: "Project-based review to mitigate fraud risks." },
                    { id: 'a5', name: "Business Entity Formation", price: 450, type: 'onetime', cat: 'consulting', desc: "Fixed fee for LLC/S-Corp registration (Excl. state fees)." },
                    { id: 'c1', name: "Action Plan Session (60m)", price: 99, type: 'onetime', cat: 'consulting', desc: "Fixed-fee consultation: Requires pre-submitted materials." },
                    { id: 'c2', name: "Ongoing Support Plan", price: 49, type: 'monthly', cat: 'consulting', desc: "Priority email/text support retainer." }
                ]
            }
        };

        const discountRules = {
            'none': { 
                name: "Standard Rates", 
                tax: 0, book_all: 0, book_mo_cap: false, all: 0, 
                privateDesc: "Standard Rates (no discount)",
                publicDesc: "Limited early client pricing may be available with an access code."
            },
            'FOUNDERS2026': { 
                name: "Founders Rate", 
                tax: 0.20, book_all: 0.20, book_mo_cap: true, all: 0,
                privateDesc: "Founders Rate applied: 20% off tax and bookkeeping services for your first 3 months.",
                publicDesc: "Limited early client pricing may be available with an access code."
            },
            'PRIDE15': { 
                name: "LGBTQ+ Community", 
                tax: 0.15, book_all: 0, book_mo_cap: false, all: 0,
                privateDesc: "LGBTQ+ Community Discount applied.",
                publicDesc: "Certain community discounts may be available with an access code."
            },
            'HENNIGFAM': { 
                name: "Family & Friends", 
                tax: 0, book_all: 0, book_mo_cap: false, all: 0.25, 
                privateDesc: "Family & Friends Discount applied.",
                publicDesc: "Private discount available only with an access code."
            }
        };

        let currentTab = 'tax';
        let quoteItems = [];
        let currentDiscountCode = 'none';
        let quoteChart = null;

        // --- RENDER LOGIC ---

        function switchTab(tabId) {
            currentTab = tabId;
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('tab-active', 'bg-stone-50');
                if(btn.id === `btn-${tabId}`) btn.classList.add('tab-active', 'bg-stone-50');
            });
            renderContent(tabId);
        }

        function renderContent(tabId) {
            const container = document.getElementById('content-area');
            
            if (tabId === 'tax') {
                renderTaxTab(container);
            } else if (tabId === 'bookkeeping') {
                renderBookkeepingTab(container);
            } else if (tabId === 'payroll') {
                renderPayrollTab(container);
            } else {
                renderGenericTab(container, tabId);
            }
        }

        // --- SPECIFIC TAB RENDERERS ---

        function renderTaxTab(container) {
            let html = `
                <div class="bg-white rounded-lg shadow-sm p-6 animate-fade-in">
                    <h2 class="text-2xl font-bold text-navy-900 mb-2">Tax Preparation</h2>
                    <p class="text-stone-600 mb-6 border-b border-stone-200 pb-4">Accurate, affordable, and transparent tax preparation. We focus on complexity-based pricing.</p>
                    <div class="grid grid-cols-1 gap-4">
            `;

            // 1. Simple Individual (Revised)
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">Simple Individual Return</h3>
                    <p class="text-sm text-stone-500 mb-3">Base Price: $225 (W-2 only, standard deduction)</p>
                    <div class="space-y-2 mb-3">
                        <label class="flex items-center gap-2 text-sm text-stone-700">
                            <input type="checkbox" id="chk_mfj" class="rounded text-forest-600"> Married Filing Jointly (+$30)
                        </label>
                        <label class="flex items-center gap-2 text-sm text-stone-700">
                            <input type="checkbox" id="chk_scha" class="rounded text-forest-600"> Itemized Deductions (Sch A) (+$75)
                        </label>
                    </div>
                    <button onclick="addSimpleReturn()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Return</button>
                </div>
            `;

            // 2. Schedule C (Business Complexity)
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">Business / Sole Proprietor (Sch C)</h3>
                    <div class="space-y-3">
                        <select id="sel_sch_c" class="w-full text-sm border-stone-300 rounded p-2 bg-stone-50">
                            <option value="299">Very Simple (+$299) - Clean, no inventory/employees</option>
                            <option value="399">Standard (+$399) - Multiple expenses/income</option>
                            <option value="499">Complex (+$499) - High volume, cash-heavy</option>
                        </select>
                        <div class="flex items-center gap-2">
                            <input type="checkbox" id="chk_sch_c_clean" class="rounded text-forest-600">
                            <label for="chk_sch_c_clean" class="text-sm text-stone-600">My books need cleanup (+$100)</label>
                        </div>
                        <button onclick="addScheduleC()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Business Return</button>
                    </div>
                </div>
            `;

            // 3. 1099-B (Stocks/Crypto)
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">Investments (Stocks/Crypto)</h3>
                    <label class="text-xs text-stone-500 block mb-1">How many trades did you have?</label>
                    <select id="sel_1099b" class="w-full text-sm border-stone-300 rounded p-2 bg-stone-50 mb-3">
                        <option value="50">1–25 trades (+$50)</option>
                        <option value="100">26–200 trades (+$100)</option>
                        <option value="custom">200+ trades (Custom Quote)</option>
                    </select>
                    <button onclick="add1099B()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Investment Fees</button>
                </div>
            `;

            // 4. Rental Properties
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">Rental Properties (Sch E)</h3>
                    <label class="text-xs text-stone-500 block mb-1">How many properties?</label>
                    <select id="sel_rentals" class="w-full text-sm border-stone-300 rounded p-2 bg-stone-50 mb-3">
                        <option value="125">1 Property (+$125)</option>
                        <option value="200">2–3 Properties (+$200)</option>
                        <option value="custom">4+ Properties (Custom Quote)</option>
                    </select>
                    <button onclick="addRentals()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Rental Fees</button>
                </div>
            `;

            // 5. State Returns (Logic Updated)
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">State Tax Returns</h3>
                    <label class="text-xs text-stone-500 block mb-1">How many states do you need to file?</label>
                    <select id="sel_states" class="w-full text-sm border-stone-300 rounded p-2 bg-stone-50 mb-3">
                        <option value="75">1 State ($75)</option>
                        <option value="150">2 States ($150)</option>
                        <option value="225">3 States ($225)</option>
                        <option value="custom">4+ States (Custom Quote)</option>
                    </select>
                    <button onclick="addStates()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add State Fees</button>
                </div>
            `;

             // 6. ITIN
             html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <h3 class="font-bold text-navy-900 mb-2">ITIN Application (W-7)</h3>
                    <label class="text-xs text-stone-500 block mb-1">Do you have a valid passport?</label>
                    <div class="flex gap-4 mb-3">
                        <label class="flex items-center gap-2 text-sm"><input type="radio" name="itin_pp" value="yes" checked> Yes ($125)</label>
                        <label class="flex items-center gap-2 text-sm"><input type="radio" name="itin_pp" value="no"> No (+$50)</label>
                    </div>
                    <button onclick="addITIN()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add ITIN Service</button>
                </div>
            `;
            
            // Partnership/S-Corp (Static)
            html += renderTaxCard({
                id: 't4', title: 'Partnership/S-Corp Tax', price: 799, 
                desc: 'Fixed fee for Form 1065 or 1120-S: Under $500k gross receipts.',
                btnAction: `addDirectItem('t4', 'Partnership/S-Corp Tax', 799, 'onetime', 'tax')`
            });

             // Tax Planning (Static)
             html += renderTaxCard({
                id: 't7', title: 'Tax Planning Session', price: 199, 
                desc: 'Dedicated consultation for proactive strategies.',
                btnAction: `addDirectItem('t7', 'Tax Planning Session', 199, 'onetime', 'tax')`
            });

            html += `</div></div>`;
            container.innerHTML = html;
        }

        function renderBookkeepingTab(container) {
            let html = `
                <div class="bg-white rounded-lg shadow-sm p-6 animate-fade-in">
                    <h2 class="text-2xl font-bold text-navy-900 mb-2">Bookkeeping Services</h2>
                    <p class="text-stone-600 mb-6 border-b border-stone-200 pb-4">Audit-Ready transactions and accurate monthly reporting.</p>
                    
                    <div class="md:col-span-2 mb-4 bg-stone-50 p-4 rounded-lg border border-stone-200">
                        <h4 class="text-sm font-bold text-navy-800 mb-2">Package Comparison</h4>
                        <div class="chart-container" style="height: 200px;"><canvas id="bookkeepingChart"></canvas></div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            `;

            // 1. Cleanup (Logic Based)
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4 flex flex-col justify-between">
                    <div>
                        <h3 class="font-bold text-navy-900 mb-1">Initial Audit & Clean-Up</h3>
                        <p class="text-sm text-stone-500 mb-3">Required for new clients.</p>
                        <label class="text-xs text-stone-500 block mb-1">How far back are your books messy?</label>
                        <select id="sel_cleanup" class="w-full text-sm border-stone-300 rounded p-2 bg-stone-50 mb-3">
                            <option value="350">1–3 months ($350)</option>
                            <option value="500">4–6 months ($500)</option>
                            <option value="650">7–12 months ($650)</option>
                            <option value="custom">12+ months (Custom)</option>
                        </select>
                    </div>
                    <button onclick="addCleanup()" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Cleanup</button>
                </div>
            `;

            // Static Bookkeeping Items
            const items = [
                { id: 'b2', name: "QuickBooks Setup", price: 200, type: 'onetime', desc: "Custom Chart of Accounts & Onboarding." },
                { id: 'b3', name: "Start-Up Essentials (Mo)", price: 199, type: 'monthly', desc: "<75 transactions, 1-2 accounts." },
                { id: 'b4', name: "Growth Standard (Mo)", price: 349, type: 'monthly', desc: "75-150 transactions, 3-4 accounts." },
                { id: 'b5', name: "Audit-Ready Premier (Mo)", price: 499, type: 'monthly', desc: "150+ trans, Accruals, Compliance." },
                { id: 'b6', name: "Accrual Conversion", price: 800, type: 'onetime', desc: "Transition from cash to accrual." }
            ];

            items.forEach(item => {
                html += renderTaxCard({
                    id: item.id, title: item.name, price: item.price, desc: item.desc,
                    btnAction: `addDirectItem('${item.id}', '${item.name}', ${item.price}, '${item.type}', 'bookkeeping')`,
                    monthly: item.type === 'monthly'
                });
            });

            html += `</div></div>`;
            container.innerHTML = html;
            setTimeout(initBookkeepingChart, 100);
        }

        function renderPayrollTab(container) {
            let html = `
                <div class="bg-white rounded-lg shadow-sm p-6 animate-fade-in">
                    <h2 class="text-2xl font-bold text-navy-900 mb-2">Payroll Services</h2>
                    <p class="text-stone-600 mb-6 border-b border-stone-200 pb-4">Flat-rate tiers with simple complexity add-ons.</p>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            `;

            // Automated Payroll
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <div class="flex justify-between items-start mb-2">
                        <h3 class="font-bold text-navy-900">Automated Payroll</h3>
                        <span class="bg-stone-100 text-navy-800 text-xs font-bold px-2 py-1 rounded">$75/mo</span>
                    </div>
                    <p class="text-sm text-stone-500 mb-4">Up to 3 employees, one pay freq, no tips/garnishments.</p>
                    <button onclick="addDirectItem('p_auto', 'Automated Payroll (Base)', 75, 'monthly', 'payroll')" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Base Plan</button>
                </div>
            `;

            // Hybrid Payroll
            html += `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4">
                    <div class="flex justify-between items-start mb-2">
                        <h3 class="font-bold text-navy-900">Hybrid Payroll</h3>
                        <span class="bg-stone-100 text-navy-800 text-xs font-bold px-2 py-1 rounded">$125/mo</span>
                    </div>
                    <p class="text-sm text-stone-500 mb-4">Up to 5 employees, tips, manual hours, inside client software.</p>
                    <button onclick="addDirectItem('p_hybrid', 'Hybrid Payroll (Base)', 125, 'monthly', 'payroll')" class="w-full bg-navy-800 hover:bg-navy-900 text-white text-sm font-bold py-2 rounded transition">Add Base Plan</button>
                </div>
            `;

            // Complexity Add-ons
            html += `
                <div class="md:col-span-2 bg-stone-50 p-4 rounded-lg border border-stone-200 mt-2">
                    <h3 class="font-bold text-navy-900 mb-3">Payroll Add-Ons & Complexity</h3>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 text-sm">
                        
                        <!-- Monthly Add-ons -->
                        <div class="space-y-2">
                            <h4 class="font-bold text-stone-600 text-xs uppercase">Monthly Add-ons</h4>
                            <div class="flex items-center justify-between">
                                <span>Add'l Employees ($10/ea)</span>
                                <input type="number" id="pay_add_emp" class="w-16 p-1 border rounded" min="0" value="0">
                            </div>
                            <div class="flex items-center justify-between">
                                <span>Contractors ($10/ea)</span>
                                <input type="number" id="pay_contractor" class="w-16 p-1 border rounded" min="0" value="0">
                            </div>
                            <div class="flex items-center justify-between">
                                <span>Multi-State ($25/state)</span>
                                <input type="number" id="pay_state" class="w-16 p-1 border rounded" min="0" value="0">
                            </div>
                            <div class="flex items-center gap-2">
                                <input type="checkbox" id="pay_tips" class="rounded"> Tips/Cash Heavy (+$25/mo)
                            </div>
                            <div class="flex items-center gap-2">
                                <input type="checkbox" id="pay_garn" class="rounded"> Garnishments (+$10/mo)
                            </div>
                        </div>

                        <!-- One-Time / Per Run -->
                        <div class="space-y-2">
                            <h4 class="font-bold text-stone-600 text-xs uppercase">Fees & Setup</h4>
                            <div class="flex items-center justify-between">
                                <span>Setup Fee</span>
                                <select id="pay_setup" class="p-1 border rounded text-xs">
                                    <option value="0">None</option>
                                    <option value="150">Basic ($150)</option>
                                    <option value="250">Standard ($250)</option>
                                    <option value="350">Complex ($350)</option>
                                </select>
                            </div>
                            <div class="flex items-center justify-between">
                                <span>Off-Cycle Runs ($25/ea)</span>
                                <input type="number" id="pay_run" class="w-16 p-1 border rounded" min="0" value="0">
                            </div>
                             <div class="flex items-center justify-between">
                                <span>Amendments ($50/ea)</span>
                                <input type="number" id="pay_amend" class="w-16 p-1 border rounded" min="0" value="0">
                            </div>
                        </div>
                    </div>
                    <button onclick="addPayrollExtras()" class="w-full bg-forest-600 hover:bg-forest-700 text-white text-sm font-bold py-2 rounded transition mt-4">Add Selected Payroll Extras</button>
                </div>
            `;

            html += `</div></div>`;
            container.innerHTML = html;
        }

        function renderGenericTab(container, tabId) {
            const data = servicesData[tabId];
            let html = `
                <div class="bg-white rounded-lg shadow-sm p-6 animate-fade-in">
                    <h2 class="text-2xl font-bold text-navy-900 mb-2">${data.title}</h2>
                    <p class="text-stone-600 mb-6 border-b border-stone-200 pb-4">${data.intro}</p>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            `;
            data.items.forEach(item => {
                html += renderTaxCard({
                    id: item.id, title: item.name, price: item.price, desc: item.desc,
                    btnAction: `addDirectItem('${item.id}', '${item.name}', ${item.price}, '${item.type}', '${item.cat}')`,
                    monthly: item.type === 'monthly'
                });
            });
            html += `</div></div>`;
            container.innerHTML = html;
        }

        function renderTaxCard({id, title, price, desc, btnAction, monthly = false}) {
            const isSelected = quoteItems.some(q => q.id === id);
            const btnClass = isSelected ? "bg-stone-400 cursor-not-allowed" : "bg-navy-800 hover:bg-navy-900";
            const btnText = isSelected ? "Added" : "Add to Quote";
            const priceDisplay = monthly ? `$${price}/mo` : `$${price}`;

            return `
                <div class="service-card bg-white border border-stone-200 rounded-lg p-4 flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="font-bold text-navy-900">${title}</h3>
                            <span class="bg-stone-100 text-navy-800 text-xs font-bold px-2 py-1 rounded">${priceDisplay}</span>
                        </div>
                        <p class="text-sm text-stone-500 mb-4">${desc}</p>
                    </div>
                    <button onclick="${btnAction}" ${isSelected ? 'disabled' : ''} class="w-full ${btnClass} text-white text-sm font-bold py-2 rounded transition">${btnText}</button>
                </div>
            `;
        }

        // --- ADD TO QUOTE LOGIC ---

        function addDirectItem(id, name, price, type, cat) {
            if (!quoteItems.some(q => q.id === id)) {
                quoteItems.push({ id, name, price, type, cat });
                updateQuote();
                if(currentTab === cat) switchTab(cat); 
                else renderContent(currentTab); 
            }
        }

        // 1. Simple Individual
        function addSimpleReturn() {
            let price = 225;
            let name = "Simple Individual Return";
            
            const mfj = document.getElementById('chk_mfj').checked;
            const scha = document.getElementById('chk_scha').checked;

            if (mfj) { price += 30; name += " (MFJ)"; }
            if (scha) { price += 75; name += " + Sch A"; }

            // Remove previous instances to prevent duplicates/stacking
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t1')); 
            
            quoteItems.push({ id: `t1_${mfj}_${scha}`, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
        }

        // 2. Schedule C
        function addScheduleC() {
            const val = parseInt(document.getElementById('sel_sch_c').value);
            const clean = document.getElementById('chk_sch_c_clean').checked;
            const price = val + (clean ? 100 : 0);
            const id = `t_sch_c_${val}_${clean ? 'clean' : 'std'}`;
            const name = `Business Return (Sch C) ${clean ? '+ Cleanup' : ''}`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t_sch_c'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
        }

        // 3. 1099-B
        function add1099B() {
            const val = document.getElementById('sel_1099b').value;
            if (val === 'custom') { alert('For 200+ trades, please contact us for a custom quote.'); return; }
            const price = parseInt(val);
            const id = `t_1099b_${price}`;
            const name = `Investment Fees (${price === 50 ? '1-25' : '26-200'} trades)`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t_1099b'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
        }

        // 4. Rentals
        function addRentals() {
            const val = document.getElementById('sel_rentals').value;
            if (val === 'custom') { alert('For 4+ properties, please contact us for a custom quote.'); return; }
            const price = parseInt(val);
            const id = `t_rent_${price}`;
            const name = `Rental Fees (${price === 125 ? '1 Prop' : '2-3 Props'})`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t_rent'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
        }

        // 5. Cleanup
        function addCleanup() {
            const val = document.getElementById('sel_cleanup').value;
            if (val === 'custom') { alert('For 12+ months backlog, please contact us for a custom quote.'); return; }
            const price = parseInt(val);
            const id = `b_clean_${price}`;
            const name = `Initial Cleanup (${val === '350' ? '1-3mo' : val === '500' ? '4-6mo' : '7-12mo'})`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('b_clean'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'bookkeeping' });
            updateQuote();
        }

        // 6. States
        function addStates() {
            const val = document.getElementById('sel_states').value;
            if (val === 'custom') { alert('For 4+ states, please contact us for a custom quote.'); return; }
            const price = parseInt(val);
            const id = `t_state_${price}`;
            const name = `State Returns (${price === 75 ? '1 State' : price === 150 ? '2 States' : '3 States'})`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t_state'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
        }

         // 7. ITIN
         function addITIN() {
            const hasPP = document.querySelector('input[name="itin_pp"]:checked').value === 'yes';
            const price = hasPP ? 125 : 175;
            const id = `t_itin_${hasPP ? 'yes' : 'no'}`;
            const name = `ITIN Application (${hasPP ? 'W/ Passport' : 'No Passport'})`;
            quoteItems = quoteItems.filter(i => !i.id.startsWith('t_itin'));
            quoteItems.push({ id, name, price, type: 'onetime', cat: 'tax' });
            updateQuote();
         }

         // 8. Payroll Extras
         function addPayrollExtras() {
            // Remove previous extras
            quoteItems = quoteItems.filter(i => i.cat !== 'payroll' || (i.id === 'p_auto' || i.id === 'p_hybrid'));

            // Monthly
            const emp = parseInt(document.getElementById('pay_add_emp').value) * 10;
            const cont = parseInt(document.getElementById('pay_contractor').value) * 10;
            const state = parseInt(document.getElementById('pay_state').value) * 25;
            const tips = document.getElementById('pay_tips').checked ? 25 : 0;
            const garn = document.getElementById('pay_garn').checked ? 10 : 0;
            
            const totalMo = emp + cont + state + tips + garn;
            if (totalMo > 0) {
                quoteItems.push({ id: 'p_extra_mo', name: 'Payroll Add-ons (Mo)', price: totalMo, type: 'monthly', cat: 'payroll' });
            }

            // One-Time
            const setup = parseInt(document.getElementById('pay_setup').value);
            const runs = parseInt(document.getElementById('pay_run').value) * 25;
            const amend = parseInt(document.getElementById('pay_amend').value) * 50;

            if (setup > 0) quoteItems.push({ id: 'p_setup', name: 'Payroll Setup Fee', price: setup, type: 'onetime', cat: 'payroll' });
            if (runs > 0) quoteItems.push({ id: 'p_runs', name: 'Off-Cycle Runs', price: runs, type: 'onetime', cat: 'payroll' });
            if (amend > 0) quoteItems.push({ id: 'p_amend', name: 'Payroll Amendments', price: amend, type: 'onetime', cat: 'payroll' });

            updateQuote();
         }


        function removeFromQuote(itemId) {
            quoteItems = quoteItems.filter(i => i.id !== itemId);
            updateQuote();
            if (servicesData[currentTab] || currentTab === 'tax' || currentTab === 'bookkeeping' || currentTab === 'payroll') renderContent(currentTab); 
        }

        function resetQuote() {
            quoteItems = [];
            document.getElementById('discount-input').value = '';
            clearDiscountCode(); 
            renderContent(currentTab);
        }
        
        // --- QUOTE & DISCOUNT LOGIC ---

        function clearDiscountCode() {
            currentDiscountCode = 'none';
            document.getElementById('discount-input').disabled = false;
            updateQuote();
        }

        function applyDiscountCode() {
            const input = document.getElementById('discount-input');
            const feedback = document.getElementById('discount-feedback');
            const code = input.value.toUpperCase().trim();

            if (discountRules[code]) {
                currentDiscountCode = code;
                input.disabled = true;
            } else {
                currentDiscountCode = 'none';
                feedback.innerText = "Code not recognized. Please check with Hennig Financial LLC.";
                feedback.classList.remove('text-forest-400', 'text-stone-400');
                feedback.classList.add('text-alert-500');
                input.disabled = false;
            }
            updateQuote();
        }

        function updateQuote() {
            const listContainer = document.getElementById('selected-items');
            const totalOneTimeEl = document.getElementById('total-onetime');
            const totalMonthlyEl = document.getElementById('total-monthly');
            const feedback = document.getElementById('discount-feedback');
            
            const rules = discountRules[currentDiscountCode] || discountRules['none']; 
            
            if (currentDiscountCode === 'none') {
                feedback.innerText = rules.publicDesc;
                feedback.classList.remove('text-forest-400', 'text-alert-500');
                feedback.classList.add('text-stone-400');
                document.getElementById('discount-input').disabled = false;
            } else {
                feedback.innerText = rules.privateDesc;
                feedback.classList.remove('text-alert-500', 'text-stone-400');
                feedback.classList.add('text-forest-400');
                document.getElementById('discount-input').disabled = true;
            }

            listContainer.innerHTML = '';
            
            let sumOneTime = 0;
            let sumMonthly = 0;
            let costTax = 0; let costBook = 0; let costOther = 0;

            if (quoteItems.length === 0) {
                listContainer.innerHTML = '<p class="text-stone-500 italic text-center py-4">Select services to build your quote.</p>';
            }

            quoteItems.forEach(item => {
                let finalPrice = item.price;
                let appliedDiscountRate = 0;

                if (rules.all > 0) {
                    appliedDiscountRate = rules.all;
                } else {
                    if (item.cat === 'tax' && rules.tax > 0) appliedDiscountRate = rules.tax;
                    else if (item.cat === 'bookkeeping') {
                        if (currentDiscountCode === 'FOUNDERS2026') {
                            if (item.type === 'onetime' && rules.book_all > 0) appliedDiscountRate = rules.book_all;
                            if (item.type === 'monthly' && rules.book_all > 0) appliedDiscountRate = rules.book_all; 
                        }
                    }
                }

                finalPrice = finalPrice * (1 - appliedDiscountRate);

                if (item.type === 'monthly') sumMonthly += finalPrice;
                else sumOneTime += finalPrice;

                const annualizedValue = item.type === 'monthly' ? finalPrice * 12 : finalPrice;
                if (item.cat === 'tax') costTax += annualizedValue;
                else if (item.cat === 'bookkeeping') costBook += annualizedValue;
                else costOther += annualizedValue;

                const div = document.createElement('div');
                div.className = 'flex justify-between items-center bg-navy-800 p-2 rounded border border-navy-700';
                
                let discountText = '';
                if (appliedDiscountRate > 0) {
                    discountText = `<div class="text-[10px] text-forest-400">Discount Applied</div>`;
                    if (currentDiscountCode === 'FOUNDERS2026' && item.cat === 'bookkeeping' && item.type === 'monthly') {
                        discountText = `<div class="text-[10px] text-forest-400">Discount Applied (3 Mo Cap)</div>`;
                    }
                }

                div.innerHTML = `
                    <div>
                        <div class="text-xs font-bold text-stone-200">${item.name}</div>
                        ${discountText}
                    </div>
                    <div class="flex items-center gap-2">
                        <span class="text-xs font-mono text-stone-300">$${Math.round(finalPrice)}</span>
                        <button onclick="removeFromQuote('${item.id}')" class="text-stone-500 hover:text-alert-500">&times;</button>
                    </div>
                `;
                listContainer.appendChild(div);
            });

            totalOneTimeEl.innerText = `$${Math.round(sumOneTime)}`;
            totalMonthlyEl.innerText = `$${Math.round(sumMonthly)}/mo`;

            updateChart(costTax, costBook, costOther);
        }

        // --- CHARTS ---

        function initBookkeepingChart() {
            const ctx = document.getElementById('bookkeepingChart');
            if (!ctx) return;
            const existingChart = Chart.getChart("bookkeepingChart");
            if (existingChart) existingChart.destroy();
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Essentials', 'Standard', 'Premier'],
                    datasets: [{
                        label: 'Included Transactions/Mo',
                        data: [75, 150, 500],
                        backgroundColor: ['#e7e5e4', '#a8a29e', '#047857'],
                        borderRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: { y: { beginAtZero: true, display: false }, x: { grid: { display: false } } }
                }
            });
        }

        function updateChart(tax, book, other) {
            const ctx = document.getElementById('quoteChart').getContext('2d');
            if (quoteChart) quoteChart.destroy();
            if (tax === 0 && book === 0 && other === 0) return;

            quoteChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Tax', 'Bookkeeping', 'Advisory/Other'],
                    datasets: [{
                        data: [tax, book, other],
                        backgroundColor: ['#1e3a8a', '#059669', '#f97316'],
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'right', labels: { color: '#e7e5e4', boxWidth: 10, font: { size: 10 } } }
                    }
                }
            });
        }

        document.addEventListener('DOMContentLoaded', () => { switchTab('tax'); });

    </script>
</body>
</html>
