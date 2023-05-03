function solution(D) {
  const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];
  const output = {};

  // Iterate over each key-value pair in the input dictionary
  for (const dateStr in D) {
    const value = D[dateStr];
    const date = new Date(dateStr);
    const dayOfWeek = daysOfWeek[date.getDay()];

    // Add the value to the corresponding day of the week
    output[dayOfWeek] = (output[dayOfWeek] || 0) + value;

    // Check if there are any missing days of the week
    const prevDate = new Date(date.getTime() - 24 * 60 * 60 * 1000);
    const nextDate = new Date(date.getTime() + 24 * 60 * 60 * 1000);
    const prevDayOfWeek = daysOfWeek[prevDate.getDay()];
    const nextDayOfWeek = daysOfWeek[nextDate.getDay()];

    if (!(prevDayOfWeek in output)) {
      output[prevDayOfWeek] = Math.round((value + (output[nextDayOfWeek] || 0)) / 2);
    }

    if (!(nextDayOfWeek in output)) {
      output[nextDayOfWeek] = Math.round((value + (output[prevDayOfWeek] || 0)) / 2);
    }
  }

  return output;
}
