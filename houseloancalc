#!/usr/bin/python
##################### 2018 标配 ############################
# 总贷款额
total_loan = 200

# 商贷利率（百分比）
sd_percent = 4.9
# 商贷利率优惠（折）
sd_discount = 95
# 商贷年限
sd_years = 30

# 公积金利率（百分比）
gjj_percent = 3.25
# 公积金贷款年限
gjj_years = 15
###########################################################


class HouseLoanCalc:
    def __init__(self, gjj_loan, gjj_years, gjj_percent, sd_loan, sd_years, sd_percent, sd_discount):
        # 公积金贷配置
        self.gjj_loan = gjj_loan
        self.gjj_years = gjj_years
        self.gjj_percent = gjj_percent
        # 商贷配置
        self.sd_loan = sd_loan
        self.sd_years = sd_years
        self.sd_percent = sd_percent
        self.sd_discount = sd_discount

    def gjj_repay_per_month(self):
        """
        公积金每月还款
        :return: 每月还款
        """
        beta = self.gjj_percent / 100 / 12
        m = self.gjj_years * 12
        return (self.gjj_loan * beta * (1 + beta) ** m / ((1 + beta) ** m - 1)) * 10000

    def sd_repay_per_month(self):
        """
        商贷每月还款
        :return: 每月还款
        """
        beta = self.sd_percent / 100 / 12
        m = self.sd_years * 12
        repayment_per_month = self.sd_loan * beta * (1 + beta) ** m / ((1 + beta) ** m - 1)
        return (repayment_per_month * self.sd_discount / 100) * 10000

    def repayment_per_month(self):
        """
            每月还款
            :return: 每月还款
        """
        return self.gjj_repay_per_month() + self.sd_repay_per_month()

    def final_repayment(self):
        """
        还款终值
        :return: 终值
        """
        return self.gjj_repay_per_month() * 12 * self.gjj_years + self.sd_repay_per_month() * 12 * self.sd_years

    def print_details(self):
        print("公积金贷款：{} 商贷：{} 每月总还款数：{:.2f} ({:.2f}+{:.2f}) "
              "\n总还款金额：{:.2f}".format(self.gjj_loan, self.sd_loan, self.repayment_per_month(),
                                      self.gjj_repay_per_month(), self.sd_repay_per_month(),
                                      self.final_repayment()))


if __name__ == "__main__":
    gjj_max_loan = 100
    for gjj_loan in range(0, gjj_max_loan+10, 10):
        calc = HouseLoanCalc(gjj_loan, gjj_years, gjj_percent,
                             total_loan - gjj_loan, sd_years, sd_percent, sd_discount)
        calc.print_details()
