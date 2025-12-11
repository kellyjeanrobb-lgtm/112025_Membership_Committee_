<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Membership Dashboard</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

    <script src="https://unpkg.com/recharts/umd/Recharts.js"></script>
    
    <script src="https://unpkg.com/lucide@latest"></script>

    <style>
        body { background-color: #f8fafc; }
    </style>
</head>
<body>

    <div id="root"></div>

    <script type="text/babel">
        // --- 1. SETUP LIBRARIES ---
        // We have to "unpack" the tools since we aren't using an import statement
        const { 
            BarChart, Bar, LineChart, Line, ComposedChart, Area, PieChart, Pie,
            XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, 
            Cell, ReferenceLine, LabelList 
        } = window.Recharts;

        const { 
            Users, DollarSign, Activity, FileText, UserMinus, UserPlus, 
            TrendingDown, TrendingUp, Wallet, CheckCircle, FileCheck, 
            ClipboardList, UserCheck, ArrowRightLeft, Layers, BarChart3,
            Clock, AlertCircle, BookOpen, Info, MapPin, Calendar, User, Database
        } = window.lucide;

        // --- 2. YOUR DASHBOARD CODE STARTS HERE ---

        const MembershipDashboard = () => {
          // November Data
          const fluxData = [
            {
              name: 'Headcount',
              New: 61,
              Resigned: 53,
              Net: 8
            },
            {
              name: 'Accounts',
              New: 35,
              Resigned: 38,
              Net: -3
            }
          ];

          // Updated Pipeline Data for November
          const pipelineData = [
            { 
              name: 'Applicants', 
              value: 113, 
              fill: '#94a3b8',
              desc: 'Has completed an application AND has paid application fee $100'
            },
            { 
              name: 'Deposits/WL', 
              fullName: 'Waitlist',
              value: 18, 
              fill: '#60a5fa',
              desc: 'Has submitted deposit or is legacy and or spouse internal waitlist'
            },
            { 
              name: 'In Processing', 
              value: 111, 
              fill: '#3b82f6',
              desc: 'Pulled off waitlist to begin pre-governance review, required 30-day posting, background checks, confirm letters of recommendation'
            },
            { 
              name: 'Cmte. Review', 
              fullName: 'Committee Review',
              value: 44, 
              fill: '#2563eb',
              desc: 'Application package is submitted and under Membership Committee and/or Board Review'
            },
            { 
              name: 'Invited', 
              value: 90, 
              fill: '#1d4ed8',
              desc: 'Formally invited to join'
            }
          ];

          // November Financials
          const financials = [
            { label: 'New Deposits', value: 52300, icon: Wallet, color: 'text-emerald-600', bg: 'bg-emerald-100' },
            { label: 'Remaining Election', value: 134596, icon: DollarSign, color: 'text-blue-600', bg: 'bg-blue-100' },
            { label: 'Application Fees', value: 1600, icon: FileText, color: 'text-indigo-600', bg: 'bg-indigo-100' },
            { label: 'Reinstatements', value: 1477.54, icon: Activity, color: 'text-purple-600', bg: 'bg-purple-100' },
          ];

          // YTD Metrics - UPDATED with "Accounts in Pipeline"
          const ytdMetrics = [
            { label: 'Applications Reviewed', value: 380, icon: ClipboardList, color: 'text-blue-600', bg: 'bg-blue-50' },
            { label: 'New Members Onboarded', value: 327, icon: UserPlus, color: 'text-emerald-600', bg: 'bg-emerald-50' },
            { label: 'Total Resignations', value: 581, icon: UserMinus, color: 'text-orange-600', bg: 'bg-orange-50' },
            { label: 'Accounts in Pipeline', value: 376, icon: Database, color: 'text-violet-600', bg: 'bg-violet-50' },
            { label: 'Exception Requests', value: 22, icon: Activity, color: 'text-purple-600', bg: 'bg-purple-50' },
            { label: 'Intermediates Elected', value: 57, icon: CheckCircle, color: 'text-indigo-600', bg: 'bg-indigo-50' },
            { label: 'Jrs Transferred to Int.', value: 249, icon: UserCheck, color: 'text-cyan-600', bg: 'bg-cyan-50' },
          ];

          const newAccountsBreakdown = [
            { label: 'Family', value: 10 },
            { label: 'Family of 2', value: 2 },
            { label: 'Individual', value: 7 },
            { label: 'Individual Under 30', value: 9 },
            { label: 'Intermediate', value: 1 },
            { label: 'Nonresident Under 30', value: 2 },
            { label: 'Spouse', value: 4 },
          ];

          const resignedAccountsBreakdown = [
            { label: 'Family', value: 1 },
            { label: 'Family of 2', value: 5 },
            { label: 'Family Pref. Tier 2', value: 1 },
            { label: 'Individual', value: 11 },
            { label: 'Individual Pref. Tier 3', value: 1 },
            { label: 'Intermediate', value: 10 },
            { label: 'Intermediate Ext. School', value: 1 },
            { label: 'Nonresident', value: 2 },
            { label: 'Nonresident 30-34', value: 1 },
            { label: 'Nonresident Family', value: 2 },
            { label: 'Spouse', value: 2 },
            { label: 'Spouse Preferred', value: 1 },
          ];

          // New Data Sets (2025 History)
          const pipelineHistoryData = [
            { month: 'Jan', Applicants: 89, Waitlist: 22, Processing: 166, Committee: 35, Invited: 77 },
            { month: 'Feb', Applicants: 91, Waitlist: 14, Processing: 167, Committee: 56, Invited: 58 },
            { month: 'Mar', Applicants: 98, Waitlist: 16, Processing: 115, Committee: 90, Invited: 63 },
            { month: 'Apr', Applicants: 85, Waitlist: 14, Processing: 124, Committee: 26, Invited: 113 },
            { month: 'May', Applicants: 107, Waitlist: 8, Processing: 86, Committee: 58, Invited: 67 },
            { month: 'Jun', Applicants: 109, Waitlist: 51, Processing: 61, Committee: 30, Invited: 107 },
            { month: 'Jul', Applicants: 116, Waitlist: 25, Processing: 113, Committee: 22, Invited: 89 },
            { month: 'Aug', Applicants: 115, Waitlist: 24, Processing: 123, Committee: 26, Invited: 76 },
            { month: 'Sep', Applicants: 114, Waitlist: 57, Processing: 105, Committee: 42, Invited: 70 },
            { month: 'Oct', Applicants: 107, Waitlist: 24, Processing: 123, Committee: 35, Invited: 70 },
            { month: 'Nov', Applicants: 113, Waitlist: 18, Processing: 111, Committee: 44, Invited: 90 },
          ];

          const cashEconomicsData = [
            { month: 'Jan', AppFees: 2100, Deposits: 61200, Capital: 36000, Total: 99300 },
            { month: 'Feb', AppFees: 1400, Deposits: 65000, Capital: 102500, Total: 168900 },
            { month: 'Mar', AppFees: 1600, Deposits: 70600, Capital: 43000, Total: 115200 },
            { month: 'Apr', AppFees: 1500, Deposits: 52000, Capital: 105000, Total: 158500 },
            { month: 'May', AppFees: 1300, Deposits: 83300, Capital: 226250, Total: 310850 },
            { month: 'Jun', AppFees: 1700, Deposits: 74600, Capital: 131100, Total: 207400 },
            { month: 'Jul', AppFees: 2200, Deposits: 69700, Capital: 112296, Total: 184196 },
            { month: 'Aug', AppFees: 1400, Deposits: 83650, Capital: 85000, Total: 170050 },
            { month: 'Sep', AppFees: 2400, Deposits: 90200, Capital: 59000, Total: 151600 },
            { month: 'Oct', AppFees: 1700, Deposits: 96000, Capital: 77700, Total: 175400 },
            { month: 'Nov', AppFees: 1600, Deposits: 52300, Capital: 134596, Total: 188496 },
          ];

          const pipelineFlowData = [
            { month: 'Jan', Inflow: 52, Total: 372, Outflow: 37, Net: 15 },
            { month: 'Feb', Inflow: 25, Total: 390, Outflow: 28, Net: -3 },
            { month: 'Mar', Inflow: 25, Total: 382, Outflow: 22, Net: 3 },
            { month: 'Apr', Inflow: 25, Total: 362, Outflow: 23, Net: 2 },
            { month: 'May', Inflow: 16, Total: 326, Outflow: 49, Net: -33 },
            { month: 'Jun', Inflow: 56, Total: 358, Outflow: 39, Net: 17 },
            { month: 'Jul', Inflow: 34, Total: 365, Outflow: 35, Net: -1 },
            { month: 'Aug', Inflow: 39, Total: 364, Outflow: 18, Net: 21 },
            { month: 'Sep', Inflow: 42, Total: 388, Outflow: 21, Net: 21 },
            { month: 'Oct', Inflow: 42, Total: 359, Outflow: 26, Net: 16 },
            { month: 'Nov', Inflow: 33, Total: 376, Outflow: 35, Net: -2 },
          ];

          // --- EXAMPLE CENSUS DATA (Based on standard club demographics) ---
          const censusAgeData = [
            { name: '< 18', value: 4359, fill: '#cbd5e1' },
            { name: '18-29', value: 2180, fill: '#94a3b8' },
            { name: '30-49', value: 7629, fill: '#64748b' },
            { name: '50-69', value: 5450, fill: '#475569' },
            { name: '70+', value: 2181, fill: '#334155' },
          ];

          const censusTypeData = [
            { name: 'Family', value: 8720, fill: '#3b82f6' },
            { name: 'Individual', value: 6540, fill: '#10b981' },
            { name: 'Junior', value: 3270, fill: '#f59e0b' },
            { name: 'Nonresident', value: 2180, fill: '#6366f1' },
            { name: 'Other', value: 1089, fill: '#94a3b8' },
          ];

          const formatCurrency = (val) => new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', maximumFractionDigits: 0 }).format(val);
          const formatCurrencyPrecise = (val) => new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', minimumFractionDigits: 2 }).format(val);

          // Custom Tooltip for Pipeline to show descriptions
          const CustomPipelineTooltip = ({ active, payload }) => {
            if (active && payload && payload.length) {
              const data = payload[0].payload;
              return (
                <div className="bg-white p-3 border border-slate-200 shadow-xl rounded-lg max-w-xs z-50">
                  <p className="font-bold text-slate-900">{data.fullName || data.name}</p>
                  <p className="text-xl font-bold text-blue-600 my-1">{data.value}</p>
                  <p className="text-xs text-slate-500 leading-snug">{data.desc}</p>
                </div>
              );
            }
            return null;
          };

          return (
            <div className="min-h-screen bg-slate-50 p-4 md:p-8 font-sans text-slate-900">
              {/* Header */}
              <header className="mb-8 border-b border-slate-200 pb-6">
                <div className="flex flex-col md:flex-row md:items-center justify-between">
                  <div>
                    <h1 className="text-4xl font-extrabold text-slate-900 tracking-tight">Membership Dashboard</h1>
                    <p className="text-slate-500 mt-2 text-lg">November 2025 Performance Overview</p>
                  </div>
                  <div className="mt-6 md:mt-0 flex gap-4">
                    <div className="px-6 py-4 bg-white rounded-xl border border-slate-200 shadow-sm text-center">
                      <span className="text-xs font-bold text-slate-400 uppercase tracking-widest block mb-1">Total Members</span>
                      <div className="text-3xl font-black text-slate-800">21,799</div>
                    </div>
                    <div className="px-6 py-4 bg-white rounded-xl border border-slate-200 shadow-sm text-center">
                      <span className="text-xs font-bold text-slate-400 uppercase tracking-widest block mb-1">Total Accounts</span>
                      <div className="text-3xl font-black text-slate-800">11,550</div>
                    </div>
                  </div>
                </div>
              </header>

              {/* YTD Snapshot Section */}
              <div className="mb-10">
                <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-slate-800 w-2 h-6 mr-3 rounded-sm"></span>
                  Membership Snapshot (YTD 2025)
                </h2>
                {/* Adjusted grid for new item */}
                <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-7 gap-4"> 
                  {ytdMetrics.map((metric, idx) => (
                    <div key={idx} className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex flex-col justify-between h-full transition-shadow hover:shadow-md">
                      <div className="flex justify-between items-start mb-3">
                        <div className={`p-2.5 rounded-lg ${metric.bg}`}>
                          <metric.icon className={`w-5 h-5 ${metric.color}`} />
                        </div>
                      </div>
                      <div>
                        <div className="text-2xl font-bold text-slate-900">{metric.value}</div>
                        <div className="text-xs font-semibold text-slate-500 mt-1 leading-tight">{metric.label}</div>
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              {/* Top Level Monthly KPIs */}
              <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                <span className="bg-blue-600 w-2 h-6 mr-3 rounded-sm"></span>
                November Monthly Performance
              </h2>
              
              {/* Primary KPIs */}
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                {/* Monthly Dues */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="flex items-center justify-between mb-4">
                    <h3 className="text-sm font-semibold text-slate-500">Total Monthly Dues</h3>
                    <div className="p-2 bg-blue-50 rounded-lg">
                      <DollarSign className="w-5 h-5 text-blue-600" />
                    </div>
                  </div>
                  <div className="text-2xl font-bold text-slate-900">{formatCurrency(2824009)}</div>
                  <p className="text-xs text-slate-400 mt-1">Recurring monthly revenue</p>
                </div>

                {/* Net Monthly Dues Change */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="flex items-center justify-between mb-4">
                    <h3 className="text-sm font-semibold text-slate-500">Net Dues Change</h3>
                    <div className="p-2 bg-emerald-50 rounded-lg">
                      <TrendingUp className="w-5 h-5 text-emerald-600" />
                    </div>
                  </div>
                  <div className="text-2xl font-bold text-emerald-600">+{formatCurrencyPrecise(1477.54)}</div>
                  <p className="text-xs text-emerald-600 mt-1 flex items-center font-medium">
                    <TrendingUp className="w-3 h-3 mr-1" />
                    New Adds {'>'} Resignations
                  </p>
                </div>

                {/* New Accounts Value */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="flex items-center justify-between mb-4">
                    <h3 className="text-sm font-semibold text-slate-500">New Accounts Value</h3>
                    <div className="p-2 bg-emerald-50 rounded-lg">
                      <UserPlus className="w-5 h-5 text-emerald-600" />
                    </div>
                  </div>
                  <div className="text-2xl font-bold text-emerald-600">+{formatCurrency(8582)}</div>
                  <p className="text-xs text-slate-400 mt-1">From 35 new accounts</p>
                </div>

                {/* Resigned Value */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="flex items-center justify-between mb-4">
                    <h3 className="text-sm font-semibold text-slate-500">Resigned Value</h3>
                    <div className="p-2 bg-orange-50 rounded-lg">
                      <UserMinus className="w-5 h-5 text-orange-600" />
                    </div>
                  </div>
                  <div className="text-2xl font-bold text-orange-600">-{formatCurrency(7104)}</div>
                  <p className="text-xs text-slate-400 mt-1">From 38 resigned accounts</p>
                </div>
              </div>

              {/* Breakdown Details Row */}
              <div className="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                 {/* New Accounts Breakdown */}
                 <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm h-full">
                    <div className="flex items-center justify-between mb-4 pb-2 border-b border-slate-100">
                       <h3 className="font-bold text-slate-900">New Accounts by Type</h3>
                       <span className="px-2 py-1 bg-emerald-100 text-emerald-800 text-xs font-bold rounded-full">35 Total</span>
                    </div>
                    <div className="space-y-2">
                       {newAccountsBreakdown.map((item, idx) => (
                          <div key={idx} className="flex justify-between items-center text-sm">
                             <span className="text-slate-600">{item.label}</span>
                             <span className="font-bold text-slate-900">{item.value}</span>
                          </div>
                       ))}
                    </div>
                 </div>

                 {/* Resigned Accounts Breakdown */}
                 <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm h-full">
                    <div className="flex items-center justify-between mb-4 pb-2 border-b border-slate-100">
                       <h3 className="font-bold text-slate-900">Resignations by Type</h3>
                       <span className="px-2 py-1 bg-orange-100 text-orange-800 text-xs font-bold rounded-full">38 Total</span>
                    </div>
                    <div className="space-y-2">
                       {resignedAccountsBreakdown.map((item, idx) => (
                          <div key={idx} className="flex justify-between items-center text-sm">
                             <span className="text-slate-600">{item.label}</span>
                             <span className="font-bold text-slate-900">{item.value}</span>
                          </div>
                       ))}
                    </div>
                 </div>

                 {/* Jr to Int Transfer Metric */}
                 <div className="flex flex-col gap-4">
                     <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex-1 flex flex-col justify-center items-center text-center">
                       <div className="p-4 bg-cyan-50 rounded-full mb-3">
                          <ArrowRightLeft className="w-8 h-8 text-cyan-600" />
                       </div>
                       <div className="text-4xl font-black text-slate-900">14</div>
                       <div className="text-sm font-bold text-slate-500 uppercase tracking-wide mt-2">Junior to Intermediate</div>
                       <div className="text-xs text-slate-400 mt-1">Transfers in November</div>
                    </div>
                 </div>
              </div>

              {/* Charts Section */}
              <div className="grid grid-cols-1 xl:grid-cols-2 gap-8 mb-10">
                
                {/* Membership Flux Chart */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col">
                  <div className="mb-4">
                    <h3 className="text-lg font-bold text-slate-900">Membership Flux (Nov)</h3>
                    <p className="text-sm text-slate-500">Comparison of Inflow vs. Outflow</p>
                  </div>
                  <div className="h-64 w-full"> 
                    <ResponsiveContainer width="100%" height="100%">
                      <BarChart
                        data={fluxData}
                        margin={{ top: 20, right: 30, left: 0, bottom: 5 }}
                      >
                        <CartesianGrid strokeDasharray="3 3" vertical={false} stroke="#e2e8f0" />
                        <XAxis dataKey="name" axisLine={false} tickLine={false} tick={{fill: '#64748b', fontSize: 12}} dy={10} />
                        <YAxis axisLine={false} tickLine={false} tick={{fill: '#64748b', fontSize: 12}} />
                        <Tooltip 
                          cursor={{fill: '#f1f5f9'}}
                          contentStyle={{borderRadius: '8px', border: 'none', boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'}}
                        />
                        <Legend iconType="circle" wrapperStyle={{paddingTop: '20px'}} />
                        <ReferenceLine y={0} stroke="#94a3b8" />
                        <Bar dataKey="New" fill="#10b981" name="New (Inflow)" radius={[4, 4, 0, 0]} barSize={48} />
                        <Bar dataKey="Resigned" fill="#ef4444" name="Resigned (Outflow)" radius={[4, 4, 0, 0]} barSize={48} />
                      </BarChart>
                    </ResponsiveContainer>
                  </div>
                </div>

                {/* Membership Pipeline Funnel */}
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm flex flex-col">
                  {/* Header Area with new small tile */}
                  <div className="mb-6 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                      <h3 className="text-lg font-bold text-slate-900">Membership Pipeline</h3>
                      <p className="text-sm text-slate-500">Current Candidate Status</p>
                    </div>
                    {/* New Small Tile Next to Pipeline */}
                    <div className="flex items-center px-4 py-2 bg-blue-50 rounded-lg border border-blue-100 shadow-sm">
                        <Layers className="w-5 h-5 text-blue-600 mr-3" />
                        <div>
                            <span className="block text-[10px] font-bold text-blue-500 uppercase tracking-wider">Total Accounts</span>
                            <span className="text-lg font-bold text-blue-900 leading-none">376</span>
                        </div>
                    </div>
                  </div>
                  
                  <div className="flex-grow flex flex-col md:flex-row gap-6">
                    <div className="h-[300px] w-full md:w-1/2">
                       <ResponsiveContainer width="100%" height="100%">
                        <BarChart
                          layout="vertical"
                          data={pipelineData}
                          margin={{ top: 0, right: 30, left: 40, bottom: 0 }}
                        >
                          <CartesianGrid strokeDasharray="3 3" horizontal={false} stroke="#e2e8f0" />
                          <XAxis type="number" hide />
                          <YAxis 
                            dataKey="name" 
                            type="category" 
                            width={90} 
                            tick={{fill: '#475569', fontSize: 11, fontWeight: 600}} 
                            axisLine={false} 
                            tickLine={false} 
                          />
                          <Tooltip content={<CustomPipelineTooltip />} cursor={{fill: '#f8fafc'}} />
                          <Bar dataKey="value" radius={[0, 4, 4, 0]} barSize={32}>
                            {pipelineData.map((entry, index) => (
                              <Cell key={`cell-${index}`} fill={entry.fill} />
                            ))}
                            <LabelList dataKey="value" position="right" style={{fill: '#334155', fontSize: 12, fontWeight: 'bold'}} />
                          </Bar>
                        </BarChart>
                      </ResponsiveContainer>
                    </div>

                    <div className="w-full md:w-1/2 flex flex-col justify-center space-y-4 pr-2">
                        {pipelineData.map((item, idx) => (
                            <div key={idx} className="flex flex-col border-l-[3px] pl-3 py-1" style={{borderColor: item.fill}}>
                                <div className="flex items-baseline justify-between">
                                    <span className="text-xs font-bold text-slate-700 uppercase tracking-wide">{item.fullName || item.name}</span>
                                </div>
                                <p className="text-xs text-slate-500 leading-relaxed mt-1">{item.desc}</p>
                            </div>
                        ))}
                    </div>
                  </div>
                </div>
              </div>

              {/* Financial Details Grid */}
              <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                <span className="bg-emerald-600 w-2 h-6 mr-3 rounded-sm"></span>
                November Payments & Financial Details
              </h2>
              <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 mb-16">
                {financials.map((item, index) => (
                  <div key={index} className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm flex items-center space-x-4">
                    <div className={`p-3 rounded-full ${item.bg}`}>
                      <item.icon className={`w-6 h-6 ${item.color}`} />
                    </div>
                    <div>
                      <p className="text-sm font-semibold text-slate-500">{item.label}</p>
                      <p className="text-xl font-bold text-slate-900">{typeof item.value === 'number' ? formatCurrency(item.value) : item.value}</p>
                    </div>
                  </div>
                ))}
              </div>

              {/* 1. MAC PIPELINE: STAGE BREAKDOWN */}
              <div className="mb-12">
                <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-slate-800 w-2 h-6 mr-3 rounded-sm"></span>
                  MAC Pipeline: Stage Breakdown (2025)
                </h2>
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="h-80 w-full">
                    <ResponsiveContainer width="100%" height="100%">
                      <BarChart
                        data={pipelineHistoryData}
                        margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                      >
                        <CartesianGrid strokeDasharray="3 3" vertical={false} />
                        <XAxis dataKey="month" tick={{fill: '#64748b'}} />
                        {/* Added Y-Axis Label */}
                        <YAxis tick={{fill: '#64748b'}} label={{ value: 'Volume (Candidates)', angle: -90, position: 'insideLeft', fill: '#94a3b8' }} />
                        <Tooltip cursor={{fill: '#f1f5f9'}} contentStyle={{borderRadius: '8px', border: 'none', boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'}} />
                        <Legend />
                        <Bar dataKey="Invited" stackId="a" fill="#1d4ed8" name="Invited" />
                        <Bar dataKey="Committee" stackId="a" fill="#2563eb" name="Cmte. Review" />
                        <Bar dataKey="Processing" stackId="a" fill="#3b82f6" name="In Processing" />
                        <Bar dataKey="Waitlist" stackId="a" fill="#60a5fa" name="Waitlist" />
                        <Bar dataKey="Applicants" stackId="a" fill="#94a3b8" name="Applicants" radius={[4, 4, 0, 0]} />
                      </BarChart>
                    </ResponsiveContainer>
                  </div>
                </div>
              </div>

              {/* 2. MAC PIPELINE: CASH & CAPITAL ECONOMICS */}
              <div className="mb-12">
                <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-emerald-600 w-2 h-6 mr-3 rounded-sm"></span>
                  MAC Pipeline: Cash & Capital Economics (2025)
                </h2>
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  <div className="h-80 w-full">
                    <ResponsiveContainer width="100%" height="100%">
                      <ComposedChart
                        data={cashEconomicsData}
                        margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                      >
                        <CartesianGrid strokeDasharray="3 3" vertical={false} />
                        <XAxis dataKey="month" tick={{fill: '#64748b'}} />
                        {/* Added Y-Axis Label */}
                        <YAxis tick={{fill: '#64748b'}} tickFormatter={(val) => `$${val/1000}k`} label={{ value: 'Cash Flow ($)', angle: -90, position: 'insideLeft', fill: '#94a3b8' }} />
                        <Tooltip formatter={(value) => formatCurrency(value)} contentStyle={{borderRadius: '8px', border: 'none', boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'}} />
                        <Legend />
                        <Bar dataKey="AppFees" stackId="a" fill="#a7f3d0" name="App Fees" />
                        <Bar dataKey="Deposits" stackId="a" fill="#34d399" name="Deposits" />
                        <Bar dataKey="Capital" stackId="a" fill="#059669" name="Capital Funds" radius={[4, 4, 0, 0]} />
                        <Line type="monotone" dataKey="Total" stroke="#064e3b" strokeWidth={3} dot={{r: 4}} name="Total Entry Cash" />
                      </ComposedChart>
                    </ResponsiveContainer>
                  </div>
                </div>
              </div>

              {/* 3. PIPELINE FLOW DYNAMICS */}
              <div className="mb-12">
                <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-purple-600 w-2 h-6 mr-3 rounded-sm"></span>
                  Pipeline Flow Dynamics (2025)
                </h2>
                <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                  {/* Main Chart */}
                  <div className="h-80 w-full mb-8">
                    <ResponsiveContainer width="100%" height="100%">
                      <ComposedChart
                        data={pipelineFlowData}
                        margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                      >
                        <CartesianGrid strokeDasharray="3 3" vertical={false} />
                        <XAxis dataKey="month" tick={{fill: '#64748b'}} />
                        <YAxis yAxisId="left" tick={{fill: '#64748b'}} label={{ value: 'Movement (Count)', angle: -90, position: 'insideLeft', fill: '#94a3b8' }} />
                        <YAxis yAxisId="right" orientation="right" tick={{fill: '#64748b'}} domain={[300, 450]} label={{ value: 'Total Pool (Count)', angle: 90, position: 'insideRight', fill: '#94a3b8' }} />
                        <Tooltip contentStyle={{borderRadius: '8px', border: 'none', boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'}} />
                        <Legend />
                        <Bar yAxisId="left" dataKey="Inflow" fill="#10b981" name="New Apps (Inflow)" radius={[4, 4, 0, 0]} barSize={20} />
                        <Bar yAxisId="left" dataKey="Outflow" fill="#ef4444" name="Elected (Outflow)" radius={[4, 4, 0, 0]} barSize={20} />
                        <Line yAxisId="left" type="monotone" dataKey="Net" stroke="#8b5cf6" strokeWidth={3} dot={{r: 4}} name="Net Difference" />
                        <Area yAxisId="right" type="monotone" dataKey="Total" fill="#f1f5f9" stroke="#94a3b8" strokeDasharray="5 5" name="Total Pool Size" />
                      </ComposedChart>
                    </ResponsiveContainer>
                  </div>

                  {/* "How to Read This Chart" Guide - PROFESSIONAL */}
                  <div className="bg-slate-50 p-5 rounded-lg border border-slate-100 flex flex-col md:flex-row items-start gap-6">
                     <div className="flex-shrink-0 mt-1">
                        <div className="bg-purple-100 p-2 rounded-full">
                           <Info className="w-5 h-5 text-purple-600" />
                        </div>
                     </div>
                     <div>
                        <h4 className="font-bold text-slate-800 text-sm uppercase tracking-wide mb-2">How to Read This Chart: Flow & Inventory Dynamics</h4>
                        <p className="text-sm text-slate-600 mb-4 leading-relaxed">
                           This visualization combines <strong>Throughput (Flow)</strong> and <strong>Pipeline Volume (Inventory)</strong> to demonstrate the efficiency and capacity of our membership intake process.
                        </p>
                        <div className="grid grid-cols-1 md:grid-cols-2 gap-x-8 gap-y-3">
                           <div className="flex items-center text-sm">
                              <span className="w-3 h-3 rounded-full bg-emerald-500 mr-2"></span>
                              <span className="font-semibold text-slate-700 mr-1">Green Bars (Inflow):</span> 
                              <span className="text-slate-500">New Demand / Applications Received.</span>
                           </div>
                           <div className="flex items-center text-sm">
                              <span className="w-3 h-3 rounded-full bg-red-500 mr-2"></span>
                              <span className="font-semibold text-slate-700 mr-1">Red Bars (Outflow):</span> 
                              <span className="text-slate-500">Throughput / Members Elected.</span>
                           </div>
                           <div className="flex items-center text-sm">
                              <span className="w-3 h-3 rounded-full bg-purple-500 mr-2"></span>
                              <span className="font-semibold text-slate-700 mr-1">Purple Line (Net Flow):</span> 
                              <span className="text-slate-500">Net Accumulation (Positive = Growing Backlog).</span>
                           </div>
                           <div className="flex items-center text-sm">
                              <span className="w-3 h-3 rounded-full bg-slate-200 mr-2 border border-slate-300"></span>
                              <span className="font-semibold text-slate-700 mr-1">Grey Area (Inventory):</span> 
                              <span className="text-slate-500">Total Active Candidates in Pipeline.</span>
                           </div>
                        </div>
                     </div>
                  </div>
                </div>
              </div>

              {/* --- CURRENT MEMBERSHIP CENSUS (SNAPSHOT) --- */}
              <div className="mb-12">
                <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-sky-600 w-2 h-6 mr-3 rounded-sm"></span>
                  Current Membership Census (Snapshot)
                </h2>
                
                <div className="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
                    <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div className="flex justify-between items-start mb-2">
                            <span className="text-xs font-bold text-slate-400 uppercase tracking-widest">Avg Member Age</span>
                            <Clock className="w-5 h-5 text-sky-500" />
                        </div>
                        <div className="text-3xl font-black text-slate-800">46 <span className="text-sm font-medium text-slate-400">yrs</span></div>
                    </div>
                     <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div className="flex justify-between items-start mb-2">
                            <span className="text-xs font-bold text-slate-400 uppercase tracking-widest">Avg Tenure</span>
                            <Calendar className="w-5 h-5 text-sky-500" />
                        </div>
                        <div className="text-3xl font-black text-slate-800">12.4 <span className="text-sm font-medium text-slate-400">yrs</span></div>
                    </div>
                     <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div className="flex justify-between items-start mb-2">
                            <span className="text-xs font-bold text-slate-400 uppercase tracking-widest">Top Zip Code</span>
                            <MapPin className="w-5 h-5 text-sky-500" />
                        </div>
                        <div className="text-3xl font-black text-slate-800">97229 <span className="text-sm font-medium text-slate-400">NW PDX</span></div>
                    </div>
                     <div className="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                        <div className="flex justify-between items-start mb-2">
                            <span className="text-xs font-bold text-slate-400 uppercase tracking-widest">Gender Split</span>
                            <User className="w-5 h-5 text-sky-500" />
                        </div>
                        <div className="flex items-baseline space-x-2">
                            <div className="text-xl font-bold text-slate-800">52% M</div>
                            <div className="text-xl font-bold text-slate-800">48% F</div>
                        </div>
                    </div>
                </div>

                <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
                     <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <h3 className="font-bold text-slate-900 mb-4">Membership by Age Group</h3>
                        <div className="h-64 w-full">
                            <ResponsiveContainer width="100%" height="100%">
                                <BarChart data={censusAgeData} margin={{ top: 20, right: 30, left: 0, bottom: 5 }}>
                                    <CartesianGrid strokeDasharray="3 3" vertical={false} />
                                    <XAxis dataKey="name" tick={{fill: '#64748b', fontSize: 12}} />
                                    <YAxis hide />
                                    <Tooltip cursor={{fill: '#f8fafc'}} />
                                    <Bar dataKey="value" radius={[4, 4, 0, 0]}>
                                        {censusAgeData.map((entry, index) => (
                                            <Cell key={`cell-${index}`} fill={entry.fill} />
                                        ))}
                                        <LabelList dataKey="value" position="top" style={{fill: '#64748b', fontSize: 12}} />
                                    </Bar>
                                </BarChart>
                            </ResponsiveContainer>
                        </div>
                     </div>

                     <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <h3 className="font-bold text-slate-900 mb-4">Membership by Type</h3>
                        <div className="h-64 w-full flex">
                            <ResponsiveContainer width="100%" height="100%">
                                 <PieChart>
                                    <Pie
                                        data={censusTypeData}
                                        cx="50%"
                                        cy="50%"
                                        innerRadius={60}
                                        outerRadius={80}
                                        paddingAngle={5}
                                        dataKey="value"
                                    >
                                        {censusTypeData.map((entry, index) => (
                                            <Cell key={`cell-${index}`} fill={entry.fill} />
                                        ))}
                                    </Pie>
                                    <Tooltip />
                                    <Legend layout="vertical" verticalAlign="middle" align="right" />
                                </PieChart>
                            </ResponsiveContainer>
                        </div>
                     </div>
                </div>
              </div>

              {/* --- COMMITTEE BUSINESS SECTION --- */}
              <div className="mb-12">
                 <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                  <span className="bg-indigo-600 w-2 h-6 mr-3 rounded-sm"></span>
                  Committee Updates & Business
                </h2>
                
                <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div className="flex items-center mb-4">
                            <Activity className="w-5 h-5 text-indigo-600 mr-2" />
                            <h3 className="font-bold text-slate-900">Strategic Initiatives</h3>
                        </div>
                        <ul className="space-y-4">
                            <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Drop Points & Retention</span>
                                Resignation survey successfully launched; preliminary data collection is underway.
                            </li>
                            <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Proposer Recognition</span>
                                Program approved by Board of Trustees; implementation phase is currently in progress. Communications and Membership are developing the promotions and launch materials.
                            </li>
                        </ul>
                    </div>

                    <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                         <div className="flex items-center mb-4">
                            <BookOpen className="w-5 h-5 text-blue-600 mr-2" />
                            <h3 className="font-bold text-slate-900">New Business (5 min)</h3>
                        </div>
                        <ul className="space-y-4">
                             <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Redline Membership P&P</span>
                                Request to accept housekeeping updates aligning P&P with current Club Rules and forms. Edits focus on "At Your Service" nomenclature updates and consistency regarding Nonresident property ownership definitions.
                            </li>
                            <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Winged M December Spread</span>
                                December issue features the 2026 dues announcement alongside a strategic "Membership Value" spread, directly incorporating themes and influence from the Membership Committee.
                            </li>
                            <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Policy Review: Divorce & Separation</span>
                                Review of current workflow regarding "Delinquent Divorce" timelines and P&P adherence, including clarification on House Committee vs. Membership Committee purview for exception requests.
                            </li>
                        </ul>
                    </div>

                     <div className="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                         <div className="flex items-center mb-4">
                            <Clock className="w-5 h-5 text-slate-500 mr-2" />
                            <h3 className="font-bold text-slate-900">Old Business (5 min)</h3>
                        </div>
                        <ul className="space-y-4">
                            <li className="text-sm text-slate-600">
                                <span className="font-semibold text-slate-900 block mb-1">Initiation Fee Audit Update</span>
                                Full account audit is complete. Staff has moved to the individual outreach phase through December, with a target of final case resolutions and action plans in place by January.
                            </li>
                        </ul>
                    </div>
                </div>
              </div>
              
            </div>
          );
        };

        // --- 3. START THE DASHBOARD ---
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<MembershipDashboard />);
    </script>
</body>
</html>
