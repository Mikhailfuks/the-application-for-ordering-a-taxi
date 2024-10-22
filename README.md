// Основные элементы интерфейса
const orderButton = document.getElementById('order-button');
const pickupLocationInput = document.getElementById('pickup-location');
const destinationLocationInput = document.getElementById('destination-location');
const orderDetails = document.getElementById('order-details');

// Функция для отправки запроса на заказ такси
function orderTaxi() {
  const pickupLocation = pickupLocationInput.value;
  const destinationLocation = destinationLocationInput.value;

  // Проверка ввода
  if (!pickupLocation || !destinationLocation) {
    alert('Пожалуйста, введите места отправления и назначения.');
    return;
  }

  // Отправка запроса (заменить на ваш API)
  fetch('/api/order-taxi', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      pickupLocation,
      destinationLocation
    })
  })
  .then(response => response.json())
  .then(data => {
    // Обработка ответа API
    if (data.success) {
      orderDetails.innerHTML = `
        <h2>Заказ успешно оформлен!</h2>
        <p>Место отправления: ${pickupLocation}</p>
        <p>Место назначения: ${destinationLocation}</p>
        <p>Номер заказа: ${data.orderId}</p>
      `;
    } else {
      alert('Ошибка при оформлении заказа.');
    }
  })
  .catch(error => {
    console.error('Ошибка при отправке запроса:', error);
    alert('Произошла ошибка. Попробуйте позже.');
  });
}

// Обработчик клика по кнопке "Заказать такси"
orderButton.addEventListener('click', orderTaxi);
