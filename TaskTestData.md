namespace DiscountCalculator
{
    public class DiscountCalculator
    {
        public decimal CalculateDiscount(int points)
        {
            if (points < 0)
            {
                throw new ArgumentException("Количество баллов не может быть отрицательным.");
            }

            if (points >= 0 && points < 100)
            {
                return 0.01m; // 1%
            }
            else if (points >= 100 && points < 200)
            {
                return 0.03m; // 3%
            }
            else if (points >= 200 && points < 500)
            {
                return 0.05m; // 5%
            }
            else
            {
                return 0.10m; // 10%
            }
        }
    }
}

using NUnit.Framework;
using DiscountCalculator;
using System;

namespace DiscountCalculatorTests
{
    [TestFixture]
    public class DiscountCalculatorTests
    {
        [Test]
        [TestCase(0, 0.01)]
        [TestCase(50, 0.01)]
        [TestCase(99, 0.01)]
        [TestCase(100, 0.03)]
        [TestCase(150, 0.03)]
        [TestCase(199, 0.03)]
        [TestCase(200, 0.05)]
        [TestCase(350, 0.05)]
        [TestCase(499, 0.05)]
        [TestCase(500, 0.10)]
        [TestCase(750, 0.10)]
        [TestCase(1000, 0.10)]
        public void CalculateDiscount_ValidPoints_ReturnsCorrectDiscount(int points, decimal expectedDiscount)
        {
            DiscountCalculator calculator = new DiscountCalculator();
            decimal actualDiscount = calculator.CalculateDiscount(points);
            Assert.AreEqual(expectedDiscount, actualDiscount);
        }

        [Test]
        public void CalculateDiscount_NegativePoints_ThrowsArgumentException()
        {
            DiscountCalculator calculator = new DiscountCalculator();
            Assert.Throws<ArgumentException>(() => calculator.CalculateDiscount(-1));
        }
    }
}