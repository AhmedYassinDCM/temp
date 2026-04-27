```js
const now = new Date();
        const monthIndex = now.getMonth();
        const currentQuarter = Math.floor(monthIndex / 3) + 1;

        if (monthIndex % 3 !== 0) {
            return {
                year: now.getFullYear(),
                quarter: currentQuarter
            };
        }

        if (currentQuarter === 1) {
            return {
                year: now.getFullYear() - 1,
                quarter: 4
            };
        }

        return {
            year: now.getFullYear(),
            quarter: currentQuarter - 1
        };





```
