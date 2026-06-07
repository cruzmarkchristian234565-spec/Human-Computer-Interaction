import React, { useState } from 'react';
import { 
  LayoutDashboard, 
  Users, 
  CreditCard, 
  Settings, 
  Search, 
  Bell, 
  ChevronDown,
  ArrowUpRight,
  ArrowDownRight,
  MoreVertical,
  Plus,
  FileText,
  Activity
} from 'lucide-react';

// --- DESIGN SYSTEM COMPONENTS ---
// Structured specifically to map to Figma Components and Auto Layout

const Card = ({ children, className = "", noPadding = false }) => (
  <div className={`bg-white rounded-2xl border border-slate-200 shadow-sm flex flex-col ${noPadding ? '' : 'p-6'} ${className}`}>
    {children}
  </div>
);

const IconButton = ({ icon: Icon, className = "" }) => (
  <button className={`p-2 rounded-lg text-slate-500 hover:bg-slate-100 transition-colors flex items-center justify-center ${className}`}>
    <Icon size={20} />
  </button>
);

const Badge = ({ children, variant = "default" }) => {
  const variants = {
    default: "bg-slate-100 text-slate-700",
    success: "bg-emerald-50 text-emerald-700 border border-emerald-200",
    warning: "bg-amber-50 text-amber-700 border border-amber-200",
  };
  return (
    <span className={`px-2.5 py-1 rounded-full text-xs font-medium flex items-center gap-1 ${variants[variant]}`}>
      {children}
    </span>
  );
};

// --- APP LAYOUT ---

export default function App() {
  const [activeMenu, setActiveMenu] = useState('Overview');

  const menuItems = [
    { name: 'Overview', icon: LayoutDashboard },
    { name: 'Analytics', icon: Activity },
    { name: 'Customers', icon: Users },
    { name: 'Transactions', icon: CreditCard },
    { name: 'Reports', icon: FileText },
  ];

  return (
    <div className="min-h-screen bg-slate-50 flex font-sans text-slate-900 w-full">
      
      {/* SIDEBAR 
        Figma Translation: Vertical Auto Layout, Fixed Width, Fill Height, Gap 8px 
      */}
      <aside className="w-64 bg-white border-r border-slate-200 flex flex-col h-screen sticky top-0">
        {/* Logo Area */}
        <div className="h-16 flex items-center px-6 border-b border-slate-100">
          <div className="flex items-center gap-2">
            <div className="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center">
              <div className="w-3 h-3 bg-white rounded-sm" />
            </div>
            <span className="font-bold text-lg tracking-tight">AcmeCorp</span>
          </div>
        </div>

        {/* Navigation */}
        <nav className="flex-1 overflow-y-auto p-4 flex flex-col gap-1">
          <div className="text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2 px-3 mt-4">Main Menu</div>
          {menuItems.map((item) => (
            <button
              key={item.name}
              onClick={() => setActiveMenu(item.name)}
              className={`flex items-center gap-3 px-3 py-2.5 rounded-xl transition-all text-sm font-medium w-full text-left
                ${activeMenu === item.name 
                  ? 'bg-indigo-50 text-indigo-700' 
                  : 'text-slate-600 hover:bg-slate-50 hover:text-slate-900'
                }`}
            >
              <item.icon size={18} className={activeMenu === item.name ? 'text-indigo-600' : 'text-slate-400'} />
              {item.name}
            </button>
          ))}
        </nav>

        {/* Bottom Actions */}
        <div className="p-4 border-t border-slate-100">
          <button className="flex items-center gap-3 px-3 py-2.5 rounded-xl transition-all text-sm font-medium w-full text-left text-slate-600 hover:bg-slate-50 hover:text-slate-900">
            <Settings size={18} className="text-slate-400" />
            Settings
          </button>
        </div>
      </aside>

      {/* MAIN CONTENT 
        Figma Translation: Vertical Auto Layout, Fill Width, Fill Height
      */}
      <main className="flex-1 flex flex-col min-w-0 overflow-hidden">
        
        {/* Top Header */}
        <header className="h-16 bg-white/80 backdrop-blur-md border-b border-slate-200 flex items-center justify-between px-8 sticky top-0 z-10">
          <div className="flex items-center gap-4 flex-1">
            <div className="relative w-96 hidden md:block">
              <Search className="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400" size={18} />
              <input 
                type="text" 
                placeholder="Search anything..." 
                className="w-full pl-10 pr-4 py-2 bg-slate-100 border-transparent focus:bg-white focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 rounded-xl text-sm outline-none transition-all"
              />
            </div>
          </div>
          
          <div className="flex items-center gap-4">
            <IconButton icon={Bell} />
            <div className="w-px h-6 bg-slate-200 mx-2" />
            <button className="flex items-center gap-3 hover:bg-slate-50 p-1.5 pr-3 rounded-full border border-transparent hover:border-slate-200 transition-all">
              <img 
                src="https://api.dicebear.com/7.x/notionists/svg?seed=Felix&backgroundColor=f8fafc" 
                alt="User" 
                className="w-8 h-8 rounded-full bg-slate-200 border border-slate-200"
              />
              <div className="text-sm font-medium hidden sm:block">Jane Doe</div>
              <ChevronDown size={16} className="text-slate-400 hidden sm:block" />
            </button>
          </div>
        </header>

        {/* Dashboard Content */}
        <div className="flex-1 overflow-y-auto p-8 flex flex-col gap-8">
          
          {/* Page Title & Actions */}
          <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h1 className="text-2xl font-bold text-slate-900">Welcome back, Jane</h1>
              <p className="text-slate-500 text-sm mt-1">Here's what's happening with your store today.</p>
            </div>
            <button className="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2.5 rounded-xl text-sm font-medium flex items-center gap-2 shadow-sm transition-colors self-start sm:self-auto">
              <Plus size={18} />
              New Report
            </button>
          </div>

          {/* KPI Cards Grid */}
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            {[
              { title: "Total Revenue", value: "$45,231.89", trend: "+20.1%", isUp: true },
              { title: "Active Users", value: "2,338", trend: "+12.4%", isUp: true },
              { title: "New Signups", value: "842", trend: "-3.1%", isUp: false },
              { title: "Active Subscriptions", value: "1,442", trend: "+8.2%", isUp: true },
            ].map((stat, i) => (
              <Card key={i} className="gap-4 hover:border-indigo-100 transition-colors cursor-default">
                <div className="flex justify-between items-start">
                  <h3 className="text-slate-500 text-sm font-medium">{stat.title}</h3>
                  <div className={`p-1.5 rounded-lg ${stat.isUp ? 'bg-emerald-50 text-emerald-600' : 'bg-rose-50 text-rose-600'}`}>
                    {stat.isUp ? <ArrowUpRight size={16} /> : <ArrowDownRight size={16} />}
                  </div>
                </div>
                <div className="flex items-baseline gap-2">
                  <span className="text-3xl font-bold tracking-tight">{stat.value}</span>
                </div>
                <div className="flex items-center gap-2 text-sm">
                  <span className={`font-medium ${stat.isUp ? 'text-emerald-600' : 'text-rose-600'}`}>
                    {stat.trend}
                  </span>
                  <span className="text-slate-400">vs last month</span>
                </div>
              </Card>
            ))}
          </div>

          {/* Bottom Section Grid */}
          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            {/* Chart Area (Mocked visually for Figma structural layout) */}
            <Card className="lg:col-span-2 gap-6 flex flex-col h-[400px]">
              <div className="flex items-center justify-between">
                <div>
                  <h2 className="text-lg font-bold">Revenue Overview</h2>
                  <p className="text-sm text-slate-500">Monthly breakdown of your earnings</p>
                </div>
                <select className="bg-slate-50 border border-slate-200 text-sm rounded-lg px-3 py-1.5 outline-none">
                  <option>This Year</option>
                  <option>Last Year</option>
                </select>
              </div>
              
              {/* Figma Translation: Horizontal Auto Layout with space-between/gap, Align Bottom */}
              <div className="flex-1 flex items-end gap-2 sm:gap-4 mt-4 pt-4 border-t border-slate-100">
                {[40, 70, 45, 90, 65, 85, 100, 60, 45, 80, 55, 75].map((height, i) => (
                  <div key={i} className="flex-1 flex flex-col items-center gap-2 group">
                    <div className="w-full bg-slate-100 rounded-t-md relative flex items-end justify-center h-full group-hover:bg-indigo-50 transition-colors">
                      <div 
                        className="w-full bg-indigo-500 rounded-t-md transition-all duration-500 ease-out group-hover:bg-indigo-600"
                        style={{ height: `${height}%` }}
                      ></div>
                    </div>
                    <span className="text-xs text-slate-400 font-medium">
                      {['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'][i]}
                    </span>
                  </div>
                ))}
              </div>
            </Card>

            {/* Recent Activity List */}
            <Card className="flex flex-col h-[400px]" noPadding>
              <div className="p-6 border-b border-slate-100 flex items-center justify-between">
                <h2 className="text-lg font-bold">Recent Transactions</h2>
                <button className="p-1 hover:bg-slate-100 rounded-md text-slate-400">
                  <MoreVertical size={18} />
                </button>
              </div>
              
              <div className="flex-1 overflow-y-auto p-2">
                {[
                  { name: "Stripe Subscription", date: "Today, 10:23 AM", amount: "+$120.00", status: "success" },
                  { name: "AWS Hosting", date: "Yesterday, 2:45 PM", amount: "-$45.00", status: "default" },
                  { name: "Upwork Escrow", date: "Oct 24, 09:12 AM", amount: "-$300.00", status: "warning" },
                  { name: "Client Payment", date: "Oct 22, 11:30 AM", amount: "+$2,400.00", status: "success" },
                  { name: "Figma License", date: "Oct 21, 04:00 PM", amount: "-$15.00", status: "default" },
                ].map((item, i) => (
                  <div key={i} className="flex items-center justify-between p-4 hover:bg-slate-50 rounded-xl transition-colors cursor-pointer">
                    <div className="flex items-center gap-4">
                      <div className="w-10 h-10 rounded-full bg-indigo-50 text-indigo-600 flex items-center justify-center font-bold text-sm">
                        {item.name.charAt(0)}
                      </div>
                      <div>
                        <div className="font-medium text-sm text-slate-900">{item.name}</div>
                        <div className="text-xs text-slate-500 mt-0.5">{item.date}</div>
                      </div>
                    </div>
                    <div className="flex flex-col items-end gap-1">
                      <span className={`text-sm font-bold ${item.amount.startsWith('+') ? 'text-emerald-600' : 'text-slate-900'}`}>
                        {item.amount}
                      </span>
                      <Badge variant={item.status}>{item.status === 'success' ? 'Completed' : item.status === 'warning' ? 'Pending' : 'Processed'}</Badge>
                    </div>
                  </div>
                ))}
              </div>
            </Card>

          </div>
        </div>
      </main>
    </div>
  );
}
