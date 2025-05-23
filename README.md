<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重庆356路公交优化方案评价</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
    
    <!-- Tailwind 配置 -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#165DFF',
                        secondary: '#36CFC9',
                        accent: '#722ED1',
                        neutral: {
                            100: '#F5F7FA',
                            200: '#E5E6EB',
                            300: '#C9CDD4',
                            400: '#86909C',
                            500: '#4E5969',
                            600: '#272E3B',
                            700: '#1D2129',
                        }
                    },
                    fontFamily: {
                        inter: ['Inter', 'system-ui', 'sans-serif'],
                    },
                    boxShadow: {
                        'card': '0 10px 30px -5px rgba(0, 0, 0, 0.1)',
                        'hover': '0 20px 40px -5px rgba(0, 0, 0, 0.15)',
                    }
                },
            }
        }
    </script>
    
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .text-shadow {
                text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            }
            .animate-fade-in {
                animation: fadeIn 0.5s ease-in-out;
            }
            .animate-slide-up {
                animation: slideUp 0.5s ease-out;
            }
            .animate-pulse-slow {
                animation: pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite;
            }
            .scroll-smooth {
                scroll-behavior: smooth;
            }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes slideUp {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
    </style>
</head>
<body class="font-inter bg-neutral-100 text-neutral-700 scroll-smooth">
    <!-- 导航栏 -->
    <nav id="navbar" class="fixed w-full bg-white/90 backdrop-blur-md shadow-sm z-50 transition-all duration-300">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0 text-primary font-bold text-xl">
                        <i class="fa-solid fa-bus mr-2"></i>公交优化分析
                    </div>
                </div>
                
                <!-- 桌面导航 -->
                <div class="hidden md:block">
                    <div class="ml-10 flex items-center space-x-4">
                        <a href="#header" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">首页</a>
                        <a href="#basic-info" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">基础信息</a>
                        <a href="#current-analysis" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">现状分析</a>
                        <a href="#optimization" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">优化方案</a>
                        <a href="#conclusion" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">结论建议</a>
                        <a href="#contact" class="text-neutral-600 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors duration-200">数据支持</a>
                    </div>
                </div>
                
                <!-- 移动端菜单按钮 -->
                <div class="md:hidden">
                    <button id="menu-toggle" class="text-neutral-600 hover:text-primary focus:outline-none">
                        <i class="fa-solid fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- 移动端菜单 -->
        <div id="mobile-menu" class="hidden md:hidden bg-white shadow-lg animate-fade-in">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#header" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">首页</a>
                <a href="#basic-info" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">基础信息</a>
                <a href="#current-analysis" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">现状分析</a>
                <a href="#optimization" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">优化方案</a>
                <a href="#conclusion" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">结论建议</a>
                <a href="#contact" class="text-neutral-600 hover:text-primary block px-3 py-2 rounded-md text-base font-medium">数据支持</a>
            </div>
        </div>
    </nav>

    <!-- 头部区域 -->
    <header id="header" class="pt-24 pb-16 md:pt-32 md:pb-24 bg-gradient-to-br from-primary/90 to-primary text-white">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row items-center">
                <div class="md:w-1/2 mb-8 md:mb-0 animate-fade-in">
                    <h1 class="text-[clamp(2rem,5vw,3.5rem)] font-bold leading-tight text-shadow">
                        重庆356路公交优化方案评价
                    </h1>
                    <p class="mt-4 text-lg md:text-xl text-white/90 max-w-xl">
                        公交线路服务效能优化对比分析
                    </p>
                </div>
                <div class="md:w-1/2 animate-slide-up">
                    <div class="bg-white/10 backdrop-blur-sm rounded-xl p-4 shadow-lg">
                        <img src="https://picsum.photos/id/1071/600/400" alt="重庆356路公交" class="rounded-lg shadow-md w-full h-auto">
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- 主内容区域 -->
    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-12">
        <!-- 基础信息部分 -->
        <section id="basic-info" class="mb-16 animate-fade-in">
            <div class="bg-white rounded-2xl shadow-card p-6 md:p-8 transition-all duration-300 hover:shadow-hover">
                <h2 class="text-2xl md:text-3xl font-bold text-neutral-700 mb-6 border-b-2 border-primary/20 pb-3">
                    <span class="inline-block w-8 h-8 bg-primary text-white rounded-full text-center mr-2">1</span>
                    线路基础信息
                </h2>
                
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-neutral-200">
                        <thead class="bg-neutral-100">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">类别</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">字段名称</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">数据详情</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-neutral-200">
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700" rowspan="7">基础信息</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">公交名称</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">356路 (珊瑚村 -- 八公里)</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">公交ID</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">500100011661</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">城市代码</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">023</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">运营公司</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">重庆公交集团第三客运分公司</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">起始站</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">珊瑚村</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">终点站</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">八公里</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">线路距离</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">6.096公里</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>
        
        <!-- 现状分析部分 -->
        <section id="current-analysis" class="mb-16 animate-fade-in" style="animation-delay: 0.2s">
            <div class="bg-white rounded-2xl shadow-card p-6 md:p-8 transition-all duration-300 hover:shadow-hover">
                <h2 class="text-2xl md:text-3xl font-bold text-neutral-700 mb-6 border-b-2 border-primary/20 pb-3">
                    <span class="inline-block w-8 h-8 bg-primary text-white rounded-full text-center mr-2">2</span>
                    线路现状分析
                </h2>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-xl font-bold text-neutral-700 mb-4 flex items-center">
                            <i class="fa-solid fa-people-roof text-primary mr-2"></i>
                            客流特征
                        </h3>
                        <ul class="space-y-3">
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-3"></i>
                                <span>时空分布不均：早高峰八公里上车8人，晚高峰轨道六公里站下车45人</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-3"></i>
                                <span>异常站点：二塘站停站1分09秒（平均25秒），南湖路与南湖路1站间距仅0.22km</span>
                            </li>
                        </ul>
                    </div>
                    
                    <div>
                        <h3 class="text-xl font-bold text-neutral-700 mb-4 flex items-center">
                            <i class="fa-solid fa-chart-line text-primary mr-2"></i>
                            关键指标
                        </h3>
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-neutral-200">
                                <thead class="bg-neutral-100">
                                    <tr>
                                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">指标</th>
                                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">现状数据</th>
                                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">理想值</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-neutral-200">
                                    <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">平均运行速度</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">12.1km/h</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">15-20km/h</td>
                                    </tr>
                                    <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">准点率</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">65%</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">≥85%</td>
                                    </tr>
                                    <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">单位客流成本</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">1.2元/人次</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">-</td>
                                    </tr>
                                    <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">碳排放强度</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">0.1kg/人次</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">-</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
                
                <div class="mt-8">
                    <h3 class="text-xl font-bold text-neutral-700 mb-6 flex items-center">
                        <i class="fa-solid fa-chart-pie text-primary mr-2"></i>
                        现状指标可视化
                    </h3>
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm">
                        <canvas id="currentMetricsChart" width="400" height="200"></canvas>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- 优化方案部分 -->
        <section id="optimization" class="mb-16 animate-fade-in" style="animation-delay: 0.4s">
            <div class="bg-white rounded-2xl shadow-card p-6 md:p-8 transition-all duration-300 hover:shadow-hover">
                <h2 class="text-2xl md:text-3xl font-bold text-neutral-700 mb-6 border-b-2 border-primary/20 pb-3">
                    <span class="inline-block w-8 h-8 bg-primary text-white rounded-full text-center mr-2">3</span>
                    优化方案对比
                </h2>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm border-l-4 border-yellow-500 transition-all duration-300 hover:shadow-md">
                        <h3 class="text-xl font-bold text-neutral-700 mb-3 flex items-center">
                            <i class="fa-solid fa-bolt text-yellow-500 mr-2"></i>
                            方案一：基础优化
                        </h3>
                        <p class="text-neutral-600 mb-4">核心措施：合并站点、加密班次、增设换乘标识</p>
                        <ul class="space-y-2">
                            <li class="flex items-start">
                                <i class="fa-solid fa-check-circle text-green-500 mt-1 mr-2"></i>
                                <span>高峰期发车间隔缩至10分钟，增加2辆区间车</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-check-circle text-green-500 mt-1 mr-2"></i>
                                <span>日均成本增加600元，预计1.5年回本</span>
                            </li>
                        </ul>
                    </div>
                    
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm border-l-4 border-purple-500 transition-all duration-300 hover:shadow-md">
                        <h3 class="text-xl font-bold text-neutral-700 mb-3 flex items-center">
                            <i class="fa-solid fa-robot text-purple-500 mr-2"></i>
                            方案二：智能升级
                        </h3>
                        <p class="text-neutral-600 mb-4">核心措施：动态调度、新能源车辆、公交专用道</p>
                        <ul class="space-y-2">
                            <li class="flex items-start">
                                <i class="fa-solid fa-check-circle text-green-500 mt-1 mr-2"></i>
                                <span>AI算法实时调整发车间隔，最小8分钟</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-check-circle text-green-500 mt-1 mr-2"></i>
                                <span>引入新能源电动车，碳排放强度下降50%</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-check-circle text-green-500 mt-1 mr-2"></i>
                                <span>初期投入超90万元，依赖政策补贴</span>
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div class="overflow-x-auto mb-8">
                    <table class="min-w-full divide-y divide-neutral-200">
                        <thead class="bg-neutral-100">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案维度</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案一：基础优化（现状改良）</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案二：智能升级（技术驱动）</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-neutral-200">
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">调度策略</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">高峰期发车间隔从 15 分钟缩至 10 分钟，增加 2 辆区间车</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">动态调度：AI 算法实时调整发车间隔，高峰期最小间隔 8 分钟</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">站点优化</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">合并南湖路与南湖路 1 站，增设换乘标识</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">新增公交专用道（轨道六公里段），智能候车亭实时显示拥挤度</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">车辆配置</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">常规燃油车，大站快车模式</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">新能源电动车，车载客流计数器实时上传数据</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">成本投入</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">日均增加 600 元（租赁 + 改造）</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">日均增加 1200 元（智能系统 + 新能源车）</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <h3 class="text-xl font-bold text-neutral-700 mb-4 flex items-center">
                    <i class="fa-solid fa-table-columns text-primary mr-2"></i>
                    综合对比表
                </h3>
                
                <div class="overflow-x-auto mb-8">
                    <table class="min-w-full divide-y divide-neutral-200">
                        <thead class="bg-neutral-100">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">优势</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">局限性</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">适用场景</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-neutral-200">
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">现状</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">成本低、易维持</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">服务质量差、乘客流失严重</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">短期无优化预算时</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">方案一：基础优化</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">成本适中、见效快解决核心痛点（满载率、换乘）</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">依赖人工调度，长期效率提升有限无硬件升级</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">中小城市公交线路常规改造</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">方案二：智能升级</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">服务效能显著提升低碳环保、技术驱动</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">一次性投入高需政策与技术协同（如专用道、数据互通）</td>
                                <td class="px-6 py-4 text-sm text-neutral-600">大城市干线公交或试点线路</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-neutral-200">
                        <thead class="bg-neutral-100">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">维度</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">现状</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案一</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-neutral-500 uppercase tracking-wider">方案二</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-neutral-200">
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">高峰满载率</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">120%（超载）</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">≤95%</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">≤85%</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">准点率</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">65%</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">85%</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">95%</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">单位客流成本</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">1.2元/人次</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">1.12元/人次</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">1.05元/人次</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-neutral-700">碳排放强度</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">0.1kg/人次</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">0.08kg/人次</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-neutral-600">0.05kg/人次</td>
                            </tr>
                            <tr class="hover:bg-neutral-50 transition-colors duration-150">
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-semibold text-neutral-700">综合得分</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-semibold text-red-500">65.5分</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-semibold text-yellow-600">82.6分</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-semibold text-green-600">86.3分</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                
                <div class="mt-8">
                    <h3 class="text-xl font-bold text-neutral-700 mb-6 flex items-center">
                        <i class="fa-solid fa-comparison text-primary mr-2"></i>
                        方案效果对比图
                    </h3>
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm">
                        <canvas id="comparisonChart" width="400" height="200"></canvas>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- 结论与建议部分 -->
        <section id="conclusion" class="mb-16 animate-fade-in" style="animation-delay: 0.6s">
            <div class="bg-white rounded-2xl shadow-card p-6 md:p-8 transition-all duration-300 hover:shadow-hover">
                <h2 class="text-2xl md:text-3xl font-bold text-neutral-700 mb-6 border-b-2 border-primary/20 pb-3">
                    <span class="inline-block w-8 h-8 bg-primary text-white rounded-full text-center mr-2">4</span>
                    结论与建议
                </h2>
                
                <div class="bg-primary/5 rounded-xl p-6 border-l-4 border-primary mb-8">
                    <div class="flex flex-col md:flex-row">
                        <div class="md:w-1/4 mb-4 md:mb-0">
                            <div class="text-center">
                                <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-primary/10 text-primary mb-2">
                                    <i class="fa-solid fa-lightbulb text-2xl"></i>
                                </div>
                                <h3 class="font-bold text-lg">核心建议</h3>
                            </div>
                        </div>
                        <div class="md:w-3/4 md:pl-8">
                            <ul class="space-y-4">
                                <li class="flex items-start">
                                    <span class="bg-primary text-white text-xs font-bold px-2 py-1 rounded mr-3 mt-0.5">立即实施</span>
                                    <span>实施方案一，同步启动方案二的政策申报与技术筹备（如新能源车选型、数据接口申请）；</span>
                                </li>
                                <li class="flex items-start">
                                    <span class="bg-yellow-500 text-white text-xs font-bold px-2 py-1 rounded mr-3 mt-0.5">3个月内</span>
                                    <span>完成联程票试点，量化换乘量增长数据，为方案二的补贴申请提供依据；</span>
                                </li>
                                <li class="flex items-start">
                                    <span class="bg-green-500 text-white text-xs font-bold px-2 py-1 rounded mr-3 mt-0.5">长期</span>
                                    <span>建立效益追踪机制，每月监测满载率、准点率等指标，每季度调整调度策略，确保优化效果可量化、可验证。</span>
                                </li>
                            </ul>
                            <p class="mt-4 text-neutral-700">
                                通过 “短平快方案打底 + 长期方案蓄能” 的组合策略，可在风险可控的前提下最大化公交服务效能提升的可行性。
                            </p>
                        </div>
                    </div>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm">
                        <h3 class="text-lg font-bold text-neutral-700 mb-4 flex items-center">
                            <i class="fa-solid fa-check-circle text-green-500 mr-2"></i>
                            方案一实施要点
                        </h3>
                        <ul class="space-y-2">
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>优先合并南湖路与南湖路1站，缩短乘客步行距离</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>高峰期加密班次，重点保障八公里、轨道六公里等客流集中站点</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>在换乘站点增设清晰的标识和导览图，提升换乘体验</span>
                            </li>
                        </ul>
                    </div>
                    
                    <div class="bg-neutral-50 rounded-xl p-6 shadow-sm">
                        <h3 class="text-lg font-bold text-neutral-700 mb-4 flex items-center">
                            <i class="fa-solid fa-arrow-up-right-dots text-purple-500 mr-2"></i>
                            方案二筹备要点
                        </h3>
                        <ul class="space-y-2">
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>与相关部门协调申请公交专用道，重点在轨道六公里段</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>调研适合重庆地形的新能源车型，评估续航能力和维护成本</span>
                            </li>
                            <li class="flex items-start">
                                <i class="fa-solid fa-circle-dot text-primary mt-1 mr-2"></i>
                                <span>对接数据平台，建立客流实时监测系统，为AI调度算法提供数据支持</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- 页脚区域 -->
    <footer id="contact" class="bg-neutral-800 text-white py-12">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4">公交优化分析</h3>
                    <p class="text-neutral-300 mb-4">
                        本报告基于重庆356路公交线路现状，通过多维度分析提出优化方案，旨在提升公交服务质量和运营效率。
                    </p>
                    <div class="flex space-x-4">
                        <a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">
                            <i class="fa-brands fa-weixin text-xl"></i>
                        </a>
                        <a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">
                            <i class="fa-brands fa-weibo text-xl"></i>
                        </a>
                        <a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">
                            <i class="fa-brands fa-qq text-xl"></i>
                        </a>
                    </div>
                </div>
                
                <div>
                    <h3 class="text-lg font-bold mb-4">相关资源</h3>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">公交出行APP</a></li>
                        <li><a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">交通规划文件</a></li>
                        <li><a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">公众参与平台</a></li>
                        <li><a href="#" class="text-neutral-300 hover:text-white transition-colors duration-200">交通数据开放</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="text-lg font-bold mb-4">联系我们</h3>
                    <ul class="space-y-2">
                        <li class="flex items-start">
                            <i class="fa-solid fa-map-marker-alt text-primary mt-1 mr-3"></i>
                            <span class="text-neutral-300">重庆市南岸区江南大道8号</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa-solid fa-phone text-primary mt-1 mr-3"></i>
                            <span class="text-neutral-300">023-62800000</span>
                        </li>
                        <li class="flex items-start">
                            <i class="fa-solid fa-envelope text-primary mt-1 mr-3"></i>
                            <span class="text-neutral-300">contact@cqbus.com</span>
                        </li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-neutral-700 mt-8 pt-8 text-center text-neutral-400 text-sm">
                <p>© 2025 重庆公交集团第三客运分公司. 保留所有权利.</p>
            </div>
        </div>
    </footer>

    <!-- JavaScript -->
    <script>
        // 导航菜单切换
        document.getElementById('menu-toggle').addEventListener('click', function() {
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenu.classList.toggle('hidden');
        });
        
        // 导航栏滚动效果
        window.addEventListener('scroll', function() {
            const navbar = document.getElementById('navbar');
            if (window.scrollY > 100) {
                navbar.classList.add('shadow-md');
                navbar.classList.add('bg-white');
                navbar.classList.remove('bg-white/90');
            } else {
                navbar.classList.remove('shadow-md');
                navbar.classList.remove('bg-white');
                navbar.classList.add('bg-white/90');
            }
        });
        
        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                
                if (targetElement) {
                    // 关闭移动菜单（如果打开）
                    document.getElementById('mobile-menu').classList.add('hidden');
                    
                    // 滚动到目标位置
                    window.scrollTo({
                        top: targetElement.offsetTop - 80, // 考虑导航栏高度
                        behavior: 'smooth'
                    });
                }
            });
        });
        
        // 图表初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 现状指标图表
            const currentMetricsCtx = document.getElementById('currentMetricsChart').getContext('2d');
            const currentMetricsChart = new Chart(currentMetricsCtx, {
                type: 'radar',
                data: {
                    labels: ['平均运行速度', '准点率', '单位客流成本', '碳排放强度', '满载率'],
                    datasets: [{
                        label: '现状数据',
                        data: [12.1, 65, 1.2, 0.1, 120],
                        backgroundColor: 'rgba(22, 93, 255, 0.2)',
                        borderColor: 'rgba(22, 93, 255, 1)',
                        borderWidth: 2,
                        pointBackgroundColor: 'rgba(22, 93, 255, 1)',
                        pointRadius: 4
                    }, {
                        label: '理想值',
                        data: [17.5, 85, 0.8, 0.05, 80],
                        backgroundColor: 'rgba(54, 207, 201, 0.2)',
                        borderColor: 'rgba(54, 207, 201, 1)',
                        borderWidth: 2,
                        pointBackgroundColor: 'rgba(54, 207, 201, 1)',
                        pointRadius: 4
                    }]
                },
                options: {
                    scales: {
                        r: {
                            angleLines: {
                                display: true,
                                color: 'rgba(0, 0, 0, 0.1)'
                            },
                            suggestedMin: 0,
                            suggestedMax: 150,
                            ticks: {
                                stepSize: 30,
                                backdropColor: 'transparent'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'bottom'
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.parsed.r !== null) {
                                        // 根据不同指标显示不同单位
                                        if (context.label === '平均运行速度') {
                                            label += context.parsed.r + ' km/h';
                                        } else if (context.label === '准点率') {
                                            label += context.parsed.r + ' %';
                                        } else if (context.label === '单位客流成本') {
                                            label += context.parsed.r + ' 元/人次';
                                        } else if (context.label === '碳排放强度') {
                                            label += context.parsed.r + ' kg/人次';
                                        } else if (context.label === '满载率') {
                                            label += context.parsed.r + ' %';
                                        }
                                    }
                                    return label;
                                }
                            }
                        }
                    }
                }
            });
            
            // 方案对比图表
            const comparisonCtx = document.getElementById('comparisonChart').getContext('2d');
            const comparisonChart = new Chart(comparisonCtx, {
                type: 'bar',
                data: {
                    labels: ['现状', '方案一', '方案二'],
                    datasets: [
                        {
                            label: '高峰满载率 (%)',
                            data: [120, 95, 85],
                            backgroundColor: 'rgba(22, 93, 255, 0.7)',
                            borderColor: 'rgba(22, 93, 255, 1)',
                            borderWidth: 1
                        },
                        {
                            label: '准点率 (%)',
                            data: [65, 85, 95],
                            backgroundColor: 'rgba(54, 207, 201, 0.7)',
                            borderColor: 'rgba(54, 207, 201, 1)',
                            borderWidth: 1
                        },
                        {
                            label: '单位客流成本 (元/人次)',
                            data: [1.2, 1.12, 1.05],
                            backgroundColor: 'rgba(114, 46, 209, 0.7)',
                            borderColor: 'rgba(114, 46, 209, 1)',
                            borderWidth: 1
                        },
                        {
                            label: '碳排放强度 (kg/人次)',
                            data: [0.1, 0.08, 0.05],
                            backgroundColor: 'rgba(245, 158, 11, 0.7)',
                            borderColor: 'rgba(245, 158, 11, 1)',
                            borderWidth: 1
                        }
                    ]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                display: true,
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'bottom'
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
    
