🐱 CatSeedLogin-Rust - 猫种子登录系统(Rust版)
<div align="center">
https://www.rust-lang.org
https://github.com/PumpkinMC/PumpkinMC
LICENSE
https://crates.io/crates/catseedlogin-rust
🚀 高性能Rust版Minecraft登录插件 | 支持PumpkinMC服务端 | 极致性能优化
基于Rust语言开发，专为PumpkinMC服务端设计，提供原生级性能表现
</div>
📋 目录
✨ 核心功能
📥 下载安装
🎯 快速开始
📖 指令大全
🔐 权限节点
⚙️ 配置文件
🔗 多服务器配置
👨‍💻 开发者API
💬 社区支持
✨ 核心功能
🔐 安全认证
✅ 异步注册/登录系统​ - 基于Rust async/await的高性能认证
✅ Argon2密码加密​ - 采用现代加密算法，安全性更高
✅ Session管理​ - 智能会话管理，支持跨服状态保持
✅ 防暴力破解​ - 内置速率限制和尝试次数限制
🛡️ 安全防护
🔒 登录前行为限制​ - 使用PumpkinMC事件系统精确控制
🎒 物品栏保护​ - 安全的物品栏隔离机制
📍 位置同步​ - 基于PumpkinMC的实体位置管理
🕐 智能重入检测​ - 基于内存的高效玩家状态跟踪
📧 邮箱系统
📨 异步邮件发送​ - 基于Tokio的异步邮件服务
🔑 验证码管理​ - 内存安全的验证码存储和验证
📤 模板化邮件​ - 支持自定义邮件模板和内容
🌐 多服务器支持
🔄 Redis同步​ - 基于Redis Pub/Sub的跨服登录状态同步
🚪 网关控制​ - 智能的服务器间玩家流动控制
🔄 数据一致性​ - 强一致性的分布式会话管理
💾 数据存储
🗄️ 多数据库驱动​ - 支持SQLx（PostgreSQL/MySQL/SQLite）
🔄 连接池​ - 基于BB8的高性能数据库连接池
📊 性能监控​ - 内置查询性能指标收集
📥 下载安装
系统要求
Rust 1.70+
PumpkinMC 0.5+
PostgreSQL 13+ / MySQL 8.0+ / SQLite 3.35+
安装方式
Cargo安装
cargo install catseedlogin-rust
手动构建
git clone https://github.com/your-org/catseedlogin-rust.git
cd catseedlogin-rust
cargo build --release
PumpkinMC插件安装
将编译后的libcatseedlogin.so（Linux）或catseedlogin.dll（Windows）放入PumpkinMC的plugins目录
配置数据库连接和插件设置
重启PumpkinMC服务器
🎯 快速开始
基本配置
创建 config/catseedlogin.toml：
[server]
name = "my_server"
motd = "欢迎来到我的服务器"

[database]
url = "postgresql://user:pass@localhost/catseedlogin"
max_connections = 20

[security]
max_login_attempts = 5
login_timeout = 120
password_min_length = 6

[redis]
enabled = true
url = "redis://localhost:6379"
玩家指令
注册账号
/register <密码> <确认密码>
/reg <密码> <确认密码>
登录账号
/login <密码>
/l <密码>
密码管理
/changepassword <旧密码> <新密码>
/changepw <旧密码> <新密码>

/resetpassword
/repw
📖 指令大全
管理员指令
指令
权限节点
描述
/catseedlogin reload
catseedlogin.admin.reload
重载插件配置
/catseedlogin stats
catseedlogin.admin.stats
查看插件统计信息
/catseedlogin user <玩家> info
catseedlogin.admin.user.info
查看玩家信息
/catseedlogin user <玩家> resetpassword
catseedlogin.admin.user.reset
重置玩家密码
配置指令
指令
描述
默认值
/catseedlogin config set <配置项> <值>
修改运行时配置
-
/catseedlogin config get <配置项>
查看配置值
-
/catseedlogin whitelist add <指令>
添加指令白名单
-
/catseedlogin whitelist remove <指令>
移除指令白名单
-
🔐 权限节点
权限节点
描述
catseedlogin.use
使用基础登录指令
catseedlogin.email
使用邮箱功能
catseedlogin.admin.*
所有管理员权限
catseedlogin.bypass.ip_limit
绕过IP限制
catseedlogin.bypass.login
绕过登录要求
⚙️ 配置文件
主配置文件 (config/catseedlogin.toml)
[general]
# 插件基础设置
plugin_enabled = true
debug_mode = false
language = "zh_CN"

[database]
# 数据库配置
driver = "postgresql"  # postgresql, mysql, sqlite
url = "postgresql://user:pass@localhost/catseedlogin"
pool_size = 10
connect_timeout = 30

[security]
# 安全配置
password_min_length = 6
password_max_length = 32
max_login_attempts = 5
login_timeout_seconds = 120
ip_limit_count = 3
session_timeout = 3600

[email]
# 邮箱配置（可选）
enabled = false
smtp_host = "smtp.qq.com"
smtp_port = 465
username = "your-email@qq.com"
password = "your-auth-code"
from_name = "服务器名称"

[redis]
# Redis配置（多服务器模式需要）
enabled = false
url = "redis://localhost:6379"
channel_prefix = "catseedlogin"

[compatibility]
# 兼容性配置
pumpkinmc_version = "0.5"
legacy_support = false
语言文件 (lang/zh_CN.ron)
Config(
    messages: {
        "login_success": "✅ 登录成功！",
        "login_failed": "❌ 密码错误，请重试",
        "register_success": "✅ 注册成功！",
        "password_too_short": "❌ 密码长度不能少于6位",
        "ip_limit_exceeded": "❌ 同一IP下注册账号数量已达上限",
    },
    commands: {
        "reload_success": "✅ 配置重载成功",
        "reload_failed": "❌ 配置重载失败",
    },
)
🔗 多服务器配置
集群架构
# 网关服务器配置
[cluster]
mode = "gateway"
servers = [
    { name = "lobby", address = "127.0.0.1:25566" },
    { name = "survival", address = "127.0.0.1:25567" }
]

[redis]
enabled = true
url = "redis://cluster-redis:6379"
子服配置
[cluster]
mode = "child"
gateway_url = "redis://cluster-redis:6379"

[security]
verify_tokens = true
shared_secret = "your-secret-key"
👨‍💻 开发者API
事件系统
use catseedlogin::events::{LoginEvent, RegisterEvent};
use pumpkinmc::events::EventListener;

struct MyPlugin;

impl EventListener for MyPlugin {
    async fn on_player_login(&self, event: LoginEvent) {
        println!("玩家 {} 登录成功", event.player.name);
    }
    
    async fn on_player_register(&self, event: RegisterEvent) {
        println!("新玩家注册: {}", event.player.name);
    }
}
API接口
use catseedlogin::api::{CatSeedLoginAPI, PlayerAuth};

#[tokio::main]
async fn main() {
    let api = CatSeedLoginAPI::new().await.unwrap();
    
    // 检查玩家认证状态
    if let Some(auth) = api.get_player_auth("player_name").await {
        println!("玩家认证状态: {:?}", auth.is_authenticated());
    }
    
    // 强制设置密码
    api.force_set_password("player_name", "new_password").await.unwrap();
}
自定义存储后端
use catseedlogin::storage::{AuthStorage, PlayerData};
use async_trait::async_trait;

struct CustomStorage;

#[async_trait]
impl AuthStorage for CustomStorage {
    async fn get_player_data(&self, username: &str) -> Result<Option<PlayerData>> {
        // 自定义实现
        Ok(None)
    }
    
    async fn save_player_data(&self, data: &PlayerData) -> Result<()> {
        // 自定义实现
        Ok(())
    }
}
核心代码结构
主要模块
// 主入口点
pub mod catseedlogin {
    pub mod api;           // API接口
    pub mod commands;      // 指令处理
    pub mod config;        // 配置管理
    pub mod events;        // 事件系统
    pub mod storage;       // 数据存储
    pub mod security;      // 安全模块
    pub mod session;       // 会话管理
    pub mod email;         // 邮件服务
    pub mod cluster;       // 集群支持
}
核心特性实现
// 异步认证处理器
pub struct AuthHandler {
    storage: Arc<dyn AuthStorage>,
    session_manager: SessionManager,
    security: SecurityManager,
}

impl AuthHandler {
    pub async fn login(&self, username: &str, password: &str) -> Result<LoginResult> {
        // 异步登录逻辑
        self.rate_limit_check(username).await?;
        self.validate_credentials(username, password).await
    }
    
    pub async fn register(&self, username: &str, password: &str) -> Result<RegistrationResult> {
        // 异步注册逻辑
        self.validate_username(username).await?;
        self.validate_password_strength(password).await?;
        self.create_account(username, password).await
    }
}
💬 社区支持
交流渠道
GitHub Issues: 问题反馈
Discord: 开发交流群
QQ群: 123456789 (RustMC开发者交流)
贡献指南
我们欢迎社区贡献！请阅读：
贡献指南
代码规范
测试指南
性能基准测试
# 运行性能测试
cargo bench --features=benchmarks

# 生成性能报告
cargo bench --features=benchmarks -- --verbose
<div align="center">
Made with ❤️ by CatSeed-Rust Team
基于Rust语言构建的高性能Minecraft登录解决方案
https://github.com/your-org/catseedlogin-rust
</div>