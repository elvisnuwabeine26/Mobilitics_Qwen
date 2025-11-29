# Mobilitics_Qwen
Website for Mobilitics Consulting Limited developed with qwen ai

import React, { useState, useRef, useEffect } from 'react';
import { 
  BarChart3, 
  Database, 
  TrendingUp, 
  FileText, 
  Upload, 
  Link, 
  Globe, 
  Mail, 
  Phone, 
  MapPin,
  ChevronRight,
  CheckCircle,
  Star,
  Users,
  Activity,
  ArrowRight,
  BarChart2,
  LineChart,
  PieChart,
  Table,
  FileSpreadsheet,
  ExternalLink
} from 'lucide-react';
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, Line, LineChart as RechartsLineChart, PieChart as RechartsPieChart, Pie, Cell } from 'recharts';

const App = () => {
  const [activeTab, setActiveTab] = useState('services');
  const [uploadedFiles, setUploadedFiles] = useState([]);
  const [externalLinks, setExternalLinks] = useState([]);
  const [formData, setFormData] = useState({ name: '', email: '', message: '' });
  const [visualizationTab, setVisualizationTab] = useState('overview');
  const [sampleData, setSampleData] = useState([]);
  const [chartData, setChartData] = useState([]);
  const [pieData, setPieData] = useState([]);
  const fileInputRef = useRef(null);

  // Generate sample data for visualization demo
  useEffect(() => {
    // Mock sales data
    const mockData = [
      { month: 'Jan', sales: 4000, profit: 2400 },
      { month: 'Feb', sales: 3000, profit: 1398 },
      { month: 'Mar', sales: 2000, profit: 9800 },
      { month: 'Apr', sales: 2780, profit: 3908 },
      { month: 'May', sales: 1890, profit: 4800 },
      { month: 'Jun', sales: 2390, profit: 3800 },
      { month: 'Jul', sales: 3490, profit: 4300 },
    ];
    
    setSampleData(mockData);
    setChartData(mockData);
    
    // Mock category data for pie chart
    const mockPieData = [
      { name: 'Category A', value: 400 },
      { name: 'Category B', value: 300 },
      { name: 'Category C', value: 300 },
      { name: 'Category D', value: 200 },
    ];
    setPieData(mockPieData);
  }, []);

  const services = [
    {
      icon: <Database className="w-8 h-8" />,
      title: "Data Management",
      description: "Comprehensive data governance, storage, and management solutions tailored to your business needs."
    },
    {
      icon: <BarChart3 className="w-8 h-8" />,
      title: "Analytics & Insights",
      description: "Advanced analytics to transform your data into actionable business intelligence."
    },
    {
      icon: <TrendingUp className="w-8 h-8" />,
      title: "Data Visualization",
      description: "Interactive dashboards and visualizations that make complex data easy to understand."
    },
    {
      icon: <FileText className="w-8 h-8" />,
      title: "Tax Consulting",
      description: "Expert tax advisory services to ensure compliance and optimize your tax position."
    }
  ];

  const stats = [
    { value: "50+", label: "Clients Served", icon: Users },
    { value: "98%", label: "Client Satisfaction", icon: Star },
    { value: "200+", label: "Projects Completed", icon: Activity },
    { value: "5", label: "Years Experience", icon: TrendingUp }
  ];

  const COLORS = ['#0088FE', '#00C49F', '#FFBB28', '#FF8042'];

  const handleFileUpload = (event) => {
    const files = Array.from(event.target.files);
    const newFiles = files.map(file => ({
      id: Date.now() + Math.random(),
      name: file.name,
      size: file.size,
      type: file.type
    }));
    setUploadedFiles(prev => [...prev, ...newFiles]);
    
    // Simulate data processing and visualization generation
    if (files.length > 0) {
      setActiveTab('visualization');
      setVisualizationTab('charts');
    }
  };

  const handleLinkSubmit = (e) => {
    e.preventDefault();
    const linkInput = e.target.elements.link.value;
    if (linkInput) {
      setExternalLinks(prev => [...prev, {
        id: Date.now(),
        url: linkInput,
        title: `External Link ${externalLinks.length + 1}`
      }]);
      e.target.reset();
      
      // Switch to visualization tab when link is added
      setActiveTab('visualization');
      setVisualizationTab('overview');
    }
  };

  const handleContactSubmit = (e) => {
    e.preventDefault();
    alert('Thank you for your message! We will get back to you soon.');
    setFormData({ name: '', email: '', message: '' });
  };

  const renderVisualizationContent = () => {
    if (visualizationTab === 'overview') {
      return (
        <div className="space-y-6">
          <div className="bg-blue-50 border-l-4 border-blue-500 p-4 rounded-r-lg">
            <h3 className="text-lg font-semibold text-blue-800">Data Portal Overview</h3>
            <p className="text-blue-700">
              Welcome to your interactive data portal. Upload files or add external links to generate 
              real-time visualizations and analytics.
            </p>
          </div>
          
          <div className="grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-xl shadow-sm border">
              <div className="flex items-center mb-4">
                <FileSpreadsheet className="w-6 h-6 text-green-600 mr-2" />
                <h4 className="font-semibold">Uploaded Files</h4>
              </div>
              {uploadedFiles.length > 0 ? (
                <div className="space-y-2">
                  {uploadedFiles.map(file => (
                    <div key={file.id} className="flex items-center justify-between text-sm">
                      <span className="truncate">{file.name}</span>
                      <span className="text-gray-500">✓ Processed</span>
                    </div>
                  ))}
                </div>
              ) : (
                <p className="text-gray-500 text-sm">No files uploaded yet</p>
              )}
            </div>
            
            <div className="bg-white p-6 rounded-xl shadow-sm border">
              <div className="flex items-center mb-4">
                <ExternalLink className="w-6 h-6 text-purple-600 mr-2" />
                <h4 className="font-semibold">External Links</h4>
              </div>
              {externalLinks.length > 0 ? (
                <div className="space-y-2">
                  {externalLinks.map(link => (
                    <div key={link.id} className="flex items-center justify-between text-sm">
                      <a href={link.url} target="_blank" rel="noopener noreferrer" className="text-blue-600 truncate">
                        {link.title}
                      </a>
                      <ExternalLink className="w-4 h-4 text-gray-400" />
                    </div>
                  ))}
                </div>
              ) : (
                <p className="text-gray-500 text-sm">No external links added</p>
              )}
            </div>
          </div>
        </div>
      );
    }
    
    if (visualizationTab === 'charts') {
      return (
        <div className="space-y-8">
          <div className="bg-white p-6 rounded-xl shadow-sm border">
            <h3 className="text-lg font-semibold mb-4 flex items-center">
              <BarChart2 className="w-5 h-5 mr-2" />
              Sales & Profit Trends
            </h3>
            <div className="h-80">
              <ResponsiveContainer width="100%" height="100%">
                <RechartsLineChart data={chartData}>
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="month" />
                  <YAxis />
                  <Tooltip />
                  <Legend />
                  <Line type="monotone" dataKey="sales" stroke="#8884d8" activeDot={{ r: 8 }} />
                  <Line type="monotone" dataKey="profit" stroke="#82ca9d" />
                </RechartsLineChart>
              </ResponsiveContainer>
            </div>
          </div>
          
          <div className="grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-xl shadow-sm border">
              <h3 className="text-lg font-semibold mb-4 flex items-center">
                <BarChart3 className="w-5 h-5 mr-2" />
                Monthly Sales
              </h3>
              <div className="h-64">
                <ResponsiveContainer width="100%" height="100%">
                  <BarChart data={chartData}>
                    <CartesianGrid strokeDasharray="3 3" />
                    <XAxis dataKey="month" />
                    <YAxis />
                    <Tooltip />
                    <Legend />
                    <Bar dataKey="sales" fill="#3B82F6" />
                  </BarChart>
                </ResponsiveContainer>
              </div>
            </div>
            
            <div className="bg-white p-6 rounded-xl shadow-sm border">
              <h3 className="text-lg font-semibold mb-4 flex items-center">
                <PieChart className="w-5 h-5 mr-2" />
                Category Distribution
              </h3>
              <div className="h-64">
                <ResponsiveContainer width="100%" height="100%">
                  <RechartsPieChart>
                    <Pie
                      data={pieData}
                      cx="50%"
                      cy="50%"
                      labelLine={false}
                      outerRadius={80}
                      fill="#8884d8"
                      dataKey="value"
                      label={({ name, percent }) => `${name} ${(percent * 100).toFixed(0)}%`}
                    >
                      {pieData.map((entry, index) => (
                        <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                      ))}
                    </Pie>
                    <Tooltip />
                  </RechartsPieChart>
                </ResponsiveContainer>
              </div>
            </div>
          </div>
        </div>
      );
    }
    
    if (visualizationTab === 'tables') {
      return (
        <div className="bg-white rounded-xl shadow-sm border overflow-hidden">
          <div className="p-6 border-b">
            <h3 className="text-lg font-semibold flex items-center">
              <Table className="w-5 h-5 mr-2" />
              Data Table View
            </h3>
          </div>
          <div className="overflow-x-auto">
            <table className="w-full">
              <thead className="bg-gray-50">
                <tr>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Month</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Sales</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Profit</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Growth</th>
                </tr>
              </thead>
              <tbody className="bg-white divide-y divide-gray-200">
                {sampleData.map((row, index) => (
                  <tr key={index} className="hover:bg-gray-50">
                    <td className="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{row.month}</td>
                    <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${row.sales.toLocaleString()}</td>
                    <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${row.profit.toLocaleString()}</td>
                    <td className="px-6 py-4 whitespace-nowrap text-sm text-green-600">
                      {index > 0 ? (
                        `${(((sampleData[index].sales - sampleData[index-1].sales) / sampleData[index-1].sales) * 100).toFixed(1)}%`
                      ) : 'N/A'}
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
      );
    }
    
    return null;
  };

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Navigation */}
      <nav className="bg-white shadow-sm sticky top-0 z-50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            <div className="flex items-center">
              <div className="flex-shrink-0">
                <h1 className="text-2xl font-bold text-blue-600">Mobilitics</h1>
              </div>
              <div className="hidden md:block ml-10">
                <div className="flex space-x-4">
                  {['Home', 'Services', 'About', 'Contact'].map((item) => (
                    <a
                      key={item}
                      href={`#${item.toLowerCase()}`}
                      className="text-gray-600 hover:text-blue-600 px-3 py-2 rounded-md text-sm font-medium transition-colors"
                    >
                      {item}
                    </a>
                  ))}
                </div>
              </div>
            </div>
            <div className="hidden md:block">
              <button 
                onClick={() => setActiveTab('visualization')}
                className="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700 transition-colors"
              >
                Data Portal
              </button>
            </div>
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section id="home" className="bg-gradient-to-br from-blue-600 to-blue-800 text-white py-20">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="lg:grid lg:grid-cols-2 lg:gap-8 items-center">
            <div>
              <h1 className="text-4xl md:text-5xl font-bold mb-6">
                Data-Driven Solutions for Your Business
              </h1>
              <p className="text-xl mb-8 text-blue-100">
                Mobilitics Consulting Limited delivers expert data management, analytics, visualization, and tax consulting services in Uganda.
              </p>
              <div className="flex flex-col sm:flex-row gap-4">
                <button 
                  onClick={() => document.getElementById('services').scrollIntoView({ behavior: 'smooth' })}
                  className="bg-white text-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition-colors flex items-center justify-center"
                >
                  Our Services <ArrowRight className="ml-2 w-4 h-4" />
                </button>
                <button 
                  onClick={() => setActiveTab('visualization')}
                  className="border-2 border-white text-white px-8 py-3 rounded-lg font-semibold hover:bg-white hover:text-blue-600 transition-colors"
                >
                  Data Portal
                </button>
              </div>
            </div>
            <div className="mt-10 lg:mt-0 flex justify-center">
              <div className="bg-white/10 backdrop-blur-sm rounded-2xl p-8 max-w-md">
                <h3 className="text-xl font-semibold mb-4">Quick Stats</h3>
                <div className="grid grid-cols-2 gap-4">
                  {stats.map((stat, index) => (
                    <div key={index} className="text-center">
                      <div className="text-2xl font-bold">{stat.value}</div>
                      <div className="text-sm text-blue-200">{stat.label}</div>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Services Section */}
      <section id="services" className="py-20 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-3xl font-bold text-gray-900 mb-4">Our Services</h2>
            <p className="text-xl text-gray-600 max-w-3xl mx-auto">
              We provide comprehensive consulting services to help your business thrive in the data-driven world.
            </p>
          </div>
          
          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            {services.map((service, index) => (
              <div key={index} className="bg-gray-50 rounded-xl p-6 hover:shadow-lg transition-shadow">
                <div className="text-blue-600 mb-4">{service.icon}</div>
                <h3 className="text-xl font-semibold mb-3">{service.title}</h3>
                <p className="text-gray-600">{service.description}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Interactive Data Portal */}
      <section className="py-20 bg-gray-100">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-3xl font-bold text-gray-900 mb-4">Interactive Data Portal</h2>
            <p className="text-xl text-gray-600">
              Upload your data files or add external links to generate real-time visualizations and insights.
            </p>
          </div>

          <div className="bg-white rounded-2xl shadow-lg overflow-hidden">
            {/* Main Navigation Tabs */}
            <div className="flex flex-wrap gap-2 p-6 border-b">
              <button
                onClick={() => setActiveTab('upload')}
                className={`px-4 py-2 rounded-lg font-medium flex items-center ${
                  activeTab === 'upload'
                    ? 'bg-blue-600 text-white'
                    : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                }`}
              >
                <Upload className="w-4 h-4 mr-2" />
                Upload Data
              </button>
              <button
                onClick={() => setActiveTab('links')}
                className={`px-4 py-2 rounded-lg font-medium flex items-center ${
                  activeTab === 'links'
                    ? 'bg-blue-600 text-white'
                    : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                }`}
              >
                <Link className="w-4 h-4 mr-2" />
                External Links
              </button>
              <button
                onClick={() => setActiveTab('visualization')}
                className={`px-4 py-2 rounded-lg font-medium flex items-center ${
                  activeTab === 'visualization'
                    ? 'bg-blue-600 text-white'
                    : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                }`}
              >
                <BarChart3 className="w-4 h-4 mr-2" />
                Visualizations
              </button>
            </div>

            {/* Upload Tab */}
            {activeTab === 'upload' && (
              <div className="p-6 space-y-6">
                <div className="border-2 border-dashed border-gray-300 rounded-xl p-8 text-center">
                  <Upload className="w-12 h-12 text-gray-400 mx-auto mb-4" />
                  <h3 className="text-lg font-semibold mb-2">Upload Your Data Files</h3>
                  <p className="text-gray-600 mb-4">Supported formats: CSV, Excel (.xlsx, .xls), JSON</p>
                  <input
                    type="file"
                    ref={fileInputRef}
                    onChange={handleFileUpload}
                    accept=".csv,.xlsx,.xls,.json"
                    multiple
                    className="hidden"
                  />
                  <button
                    onClick={() => fileInputRef.current?.click()}
                    className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors inline-flex items-center"
                  >
                    <Upload className="w-4 h-4 mr-2" />
                    Choose Files
                  </button>
                </div>

                {uploadedFiles.length > 0 && (
                  <div className="mt-8">
                    <h4 className="text-lg font-semibold mb-4 flex items-center">
                      <CheckCircle className="w-5 h-5 text-green-500 mr-2" />
                      Successfully Uploaded Files
                    </h4>
                    <div className="space-y-3">
                      {uploadedFiles.map((file) => (
                        <div key={file.id} className="flex items-center justify-between bg-gray-50 p-3 rounded-lg">
                          <div className="flex items-center">
                            <FileSpreadsheet className="w-5 h-5 text-blue-500 mr-3" />
                            <span className="font-medium">{file.name}</span>
                            <span className="text-sm text-gray-500 ml-2">
                              ({(file.size / 1024).toFixed(1)} KB)
                            </span>
                          </div>
                          <div className="flex items-center space-x-2">
                            <span className="text-green-600 text-sm">✓ Processed</span>
                            <button className="text-blue-600 hover:text-blue-800 text-sm font-medium">
                              View
                            </button>
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>
                )}
              </div>
            )}

            {/* Links Tab */}
            {activeTab === 'links' && (
              <div className="p-6 space-y-6">
                <form onSubmit={handleLinkSubmit} className="space-y-4">
                  <div>
                    <label className="block text-sm font-medium text-gray-700 mb-2">
                      Add External Data Link
                    </label>
                    <div className="flex gap-2">
                      <input
                        type="url"
                        name="link"
                        placeholder="https://example.com/your-data-endpoint"
                        className="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                        required
                      />
                      <button
                        type="submit"
                        className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center"
                      >
                        <Link className="w-4 h-4 mr-2" />
                        Add Link
                      </button>
                    </div>
                    <p className="text-sm text-gray-500 mt-2">
                      Add URLs to JSON APIs, CSV files, or any web-accessible data source
                    </p>
                  </div>
                </form>

                {externalLinks.length > 0 && (
                  <div className="mt-8">
                    <h4 className="text-lg font-semibold mb-4 flex items-center">
                      <ExternalLink className="w-5 h-5 text-purple-500 mr-2" />
                      External Data Sources
                    </h4>
                    <div className="space-y-3">
                      {externalLinks.map((link) => (
                        <div key={link.id} className="flex items-center justify-between bg-gray-50 p-3 rounded-lg">
                          <div className="flex items-center">
                            <ExternalLink className="w-5 h-5 text-purple-500 mr-3" />
                            <a
                              href={link.url}
                              target="_blank"
                              rel="noopener noreferrer"
                              className="text-blue-600 hover:text-blue-800 font-medium truncate"
                            >
                              {link.title}
                            </a>
                          </div>
                          <div className="flex items-center space-x-2">
                            <span className="text-green-600 text-sm">✓ Connected</span>
                            <button className="text-blue-600 hover:text-blue-800 text-sm font-medium">
                              Refresh
                            </button>
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>
                )}
              </div>
            )}

            {/* Visualization Tab */}
            {activeTab === 'visualization' && (
              <div className="p-6">
                {uploadedFiles.length === 0 && externalLinks.length === 0 ? (
                  <div className="text-center py-12">
                    <BarChart3 className="w-16 h-16 text-blue-600 mx-auto mb-4" />
                    <h3 className="text-xl font-semibold mb-2">Welcome to Your Data Portal</h3>
                    <p className="text-gray-600 max-w-2xl mx-auto mb-6">
                      Upload data files or add external links to start generating visualizations. 
                      Your data will be automatically processed and displayed in various chart formats.
                    </p>
                    <div className="flex justify-center space-x-4">
                      <button
                        onClick={() => setActiveTab('upload')}
                        className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center"
                      >
                        <Upload className="w-4 h-4 mr-2" />
                        Upload Data
                      </button>
                      <button
                        onClick={() => setActiveTab('links')}
                        className="border border-blue-600 text-blue-600 px-6 py-2 rounded-lg hover:bg-blue-50 transition-colors flex items-center"
                      >
                        <Link className="w-4 h-4 mr-2" />
                        Add Link
                      </button>
                    </div>
                  </div>
                ) : (
                  <>
                    {/* Visualization Sub-tabs */}
                    <div className="flex flex-wrap gap-2 mb-6">
                      <button
                        onClick={() => setVisualizationTab('overview')}
                        className={`px-4 py-2 rounded-lg font-medium ${
                          visualizationTab === 'overview'
                            ? 'bg-blue-600 text-white'
                            : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                        }`}
                      >
                        Overview
                      </button>
                      <button
                        onClick={() => setVisualizationTab('charts')}
                        className={`px-4 py-2 rounded-lg font-medium ${
                          visualizationTab === 'charts'
                            ? 'bg-blue-600 text-white'
                            : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                        }`}
                      >
                        Charts & Graphs
                      </button>
                      <button
                        onClick={() => setVisualizationTab('tables')}
                        className={`px-4 py-2 rounded-lg font-medium ${
                          visualizationTab === 'tables'
                            ? 'bg-blue-600 text-white'
                            : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                        }`}
                      >
                        Data Tables
                      </button>
                    </div>
                    
                    {/* Visualization Content */}
                    {renderVisualizationContent()}
                  </>
                )}
              </div>
            )}
          </div>
        </div>
      </section>

      {/* About Section */}
      <section id="about" className="py-20 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="lg:grid lg:grid-cols-2 lg:gap-12 items-center">
            <div>
              <h2 className="text-3xl font-bold text-gray-900 mb-6">About Mobilitics Consulting</h2>
              <p className="text-lg text-gray-600 mb-6">
                Founded in Uganda, Mobilitics Consulting Limited specializes in providing 
                cutting-edge data management and tax consulting services to businesses across 
                East Africa and beyond.
              </p>
              <p className="text-lg text-gray-600 mb-6">
                Our team of experts combines deep technical knowledge with practical business 
                acumen to deliver solutions that drive real results for our clients.
              </p>
              <div className="flex items-center space-x-4">
                <div className="flex items-center">
                  <Globe className="w-5 h-5 text-blue-600 mr-2" />
                  <span className="text-gray-700">Based in Kampala, Uganda</span>
                </div>
                <div className="flex items-center">
                  <Users className="w-5 h-5 text-blue-600 mr-2" />
                  <span className="text-gray-700">Expert Team</span>
                </div>
              </div>
            </div>
            <div className="mt-10 lg:mt-0">
              <img
                src="https://placehold.co/600x400/3B82F6/FFFFFF?text=Uganda+Office"
                alt="Mobilitics Consulting Office"
                className="rounded-2xl shadow-lg"
              />
            </div>
          </div>
        </div>
      </section>

      {/* Contact Section */}
      <section id="contact" className="py-20 bg-gray-900 text-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-3xl font-bold mb-4">Get In Touch</h2>
            <p className="text-xl text-gray-300">
              Ready to transform your business with data-driven insights?
            </p>
          </div>

          <div className="grid md:grid-cols-2 gap-12">
            <div>
              <h3 className="text-xl font-semibold mb-6">Contact Information</h3>
              <div className="space-y-4">
                <div className="flex items-center">
                  <MapPin className="w-5 h-5 text-blue-400 mr-3" />
                  <span>Kampala, Uganda</span>
                </div>
                <div className="flex items-center">
                  <Phone className="w-5 h-5 text-blue-400 mr-3" />
                  <span>+256 XXX XXX XXX</span>
                </div>
                <div className="flex items-center">
                  <Mail className="w-5 h-5 text-blue-400 mr-3" />
                  <span>info@mobilitics.co.ug</span>
                </div>
                <div className="flex items-center">
                  <Globe className="w-5 h-5 text-blue-400 mr-3" />
                  <span>www.mobilitics.co.ug</span>
                </div>
              </div>
            </div>

            <div>
              <h3 className="text-xl font-semibold mb-6">Send us a Message</h3>
              <form onSubmit={handleContactSubmit} className="space-y-4">
                <div>
                  <input
                    type="text"
                    placeholder="Your Name"
                    value={formData.name}
                    onChange={(e) => setFormData({ ...formData, name: e.target.value })}
                    className="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    required
                  />
                </div>
                <div>
                  <input
                    type="email"
                    placeholder="Your Email"
                    value={formData.email}
                    onChange={(e) => setFormData({ ...formData, email: e.target.value })}
                    className="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    required
                  />
                </div>
                <div>
                  <textarea
                    placeholder="Your Message"
                    value={formData.message}
                    onChange={(e) => setFormData({ ...formData, message: e.target.value })}
                    rows="4"
                    className="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    required
                  />
                </div>
                <button
                  type="submit"
                  className="bg-blue-600 text-white px-8 py-3 rounded-lg hover:bg-blue-700 transition-colors w-full"
                >
                  Send Message
                </button>
              </form>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-800 text-white py-8">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col md:flex-row justify-between items-center">
            <div className="mb-4 md:mb-0">
              <h3 className="text-xl font-bold">Mobilitics Consulting Limited</h3>
              <p className="text-gray-400">Data Management & Tax Consulting Experts</p>
            </div>
            <div className="flex space-x-6">
              <a href="#" className="text-gray-400 hover:text-white transition-colors">
                Privacy Policy
              </a>
              <a href="#" className="text-gray-400 hover:text-white transition-colors">
                Terms of Service
              </a>
            </div>
          </div>
          <div className="mt-8 pt-8 border-t border-gray-700 text-center text-gray-400">
            <p>&copy; 2025 Mobilitics Consulting Limited. All rights reserved.</p>
            <p className="text-sm mt-2">Repository: <a href="https://github.com/elvisnuwabeine26/Mobilitics_Qwen" target="_blank" rel="noopener noreferrer" className="text-blue-400 hover:text-blue-300">github.com/elvisnuwabeine26/Mobilitics_Qwen</a></p>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default App;
