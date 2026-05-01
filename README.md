name: Show Visitor Alert

on:
  workflow_dispatch:
  schedule:
    - cron: '0 * * * *'  # 每小时运行一次

jobs:
  update-readme:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v4
      
    - name: Update README with visitor info
      run: |
        # 在 README 中添加醒目的提示
        cat > README.md << 'EOF'
# ⚠️ 注意：1111 ⚠️

<div align="center">
  
  ## 🚨 重要通知 🚨
  
  ### 1111
  
  ![警告](https://img.shields.io/badge/注意-1111-red?style=for-the-badge&logo=alert)
  
  ---
  
  **您正在访问此仓库！**
  
  时间: `$(date '+%Y-%m-%d %H:%M:%S')`
  
</div>

## 关于本仓库

这是一个演示仓库，用于展示访问提示功能。

## 访问统计

每次访问此 README，都会看到 "1111" 提示。

---

*最后更新: $(date '+%Y-%m-%d %H:%M:%S')*
EOF
        
    - name: Commit changes
      run: |
        git config user.name "github-actions[bot]"
        git config user.email "actions@github.com"
        git add README.md
        git diff --quiet && git diff --staged --quiet || git commit -m "更新访问提示: 1111"
        git push
