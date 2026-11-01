<script setup>
import { ref, computed, watch, onUnmounted } from 'vue'
import ClothingImage from './components/ClothingImage.vue'
import AppIcon from './components/AppIcon.vue'

const wardrobe = [
  { id: 'pink-cardigan', name: 'Pink Cardigan', category: 'Outerwear', colour: 'Pink', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#dba9ae', shape: 'top' },
  { id: 'black-trousers', name: 'Black Trousers', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#2b2a2f', shape: 'pants' },
  { id: 'grey-pleated-skirt', name: 'Grey Pleated Skirt', category: 'Bottoms', colour: 'Grey', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#8e8e90', shape: 'skirt' },
  { id: 'brown-knit-vest', name: 'Brown Knit Vest', category: 'Tops', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#7a4a32', shape: 'top' },
  { id: 'beige-skirt', name: 'Beige Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#c0a581', shape: 'skirt' },
  { id: 'black-shorts', name: 'Black Shorts', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#2c2b30', shape: 'shorts' },
  { id: 'black-heels', name: 'Black Heels', category: 'Shoes', colour: 'Black', occasion: 'Party', weather: 'Sunny', emoji: '👟', tone: '#2a292d', shape: 'shoe' },
  { id: 'leather-skirt', name: 'Leather Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Party', weather: 'Cloudy', emoji: '👗', tone: '#4d403a', shape: 'skirt' },
  { id: 'mustard-cardigan', name: 'Mustard Cardigan', category: 'Outerwear', colour: 'Yellow', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#d4a93a', shape: 'top' },
  { id: 'red-dress', name: 'Red Dress', category: 'Dresses', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#a2403b', shape: 'dress' },
  { id: 'grey-blazer', name: 'Grey Blazer', category: 'Outerwear', colour: 'Grey', occasion: 'Formal', weather: 'Sunny', emoji: '🧥', tone: '#8c8d90', shape: 'top' },
  { id: 'navy-shorts', name: 'Navy Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#34465c', shape: 'shorts' },
  { id: 'floral-dress', name: 'Floral Dress', category: 'Dresses', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#e0a4ae', shape: 'dress' },
  { id: 'pink-joggers', name: 'Pink Joggers', category: 'Bottoms', colour: 'Pink', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#e2a6b0', shape: 'pants' },
  { id: 'denim-jacket', name: 'Denim Jacket', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#4d7194', shape: 'top' },
  { id: 'beige-sweater', name: 'Beige Sweater', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#b5a48e', shape: 'top' },
  { id: 'navy-polo', name: 'Navy Polo', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#34465c', shape: 'top' },
  { id: 'striped-tee', name: 'Striped Tee', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#7d97b3', shape: 'top' },
  { id: 'purple-blouse', name: 'Purple Blouse', category: 'Tops', colour: 'Purple', occasion: 'Party', weather: 'Sunny', emoji: '👚', tone: '#7b5a9c', shape: 'blouse' },
  { id: 'white-tee', name: 'White Tee', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#e8e7e2', shape: 'top' },
  { id: 'brown-midi-dress', name: 'Brown Midi Dress', category: 'Dresses', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#6e4a36', shape: 'dress' },
  { id: 'black-crop-top', name: 'Black Crop Top', category: 'Tops', colour: 'Black', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#333137', shape: 'top' },
  { id: 'grey-hoodie', name: 'Grey Hoodie', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#7f7f7d', shape: 'top' },
  { id: 'denim-shorts', name: 'Denim Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#8aa9c4', shape: 'shorts' },
  { id: 'white-blouse', name: 'White Blouse', category: 'Tops', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👚', tone: '#ecebe6', shape: 'blouse' },
  { id: 'yellow-rain-boots', name: 'Yellow Rain Boots', category: 'Shoes', colour: 'Yellow', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#e3bf3c', shape: 'shoe' },
  { id: 'black-blouse', name: 'Black Blouse', category: 'Tops', colour: 'Black', occasion: 'Formal', weather: 'Sunny', emoji: '👚', tone: '#2d2c31', shape: 'blouse' },
  { id: 'blue-oxford-shirt', name: 'Blue Oxford Shirt', category: 'Tops', colour: 'Blue', occasion: 'Formal', weather: 'Sunny', emoji: '👕', tone: '#9bb3cc', shape: 'top' },
  { id: 'navy-loafers', name: 'Navy Loafers', category: 'Shoes', colour: 'Blue', occasion: 'Formal', weather: 'Sunny', emoji: '👟', tone: '#2f3f56', shape: 'shoe' },
  { id: 'red-sweater', name: 'Red Sweater', category: 'Tops', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#a33b36', shape: 'top' },
  { id: 'black-midi-skirt', name: 'Black Midi Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#36313a', shape: 'skirt' },
  { id: 'grey-shorts', name: 'Grey Shorts', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#9a9b9d', shape: 'shorts' },
  { id: 'brown-boots', name: 'Brown Boots', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#6a4632', shape: 'shoe' },
  { id: 'denim-skirt', name: 'Denim Skirt', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#5d88aa', shape: 'skirt' },
  { id: 'pink-sweatshirt', name: 'Pink Sweatshirt', category: 'Tops', colour: 'Pink', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#e5a9b4', shape: 'top' },
  { id: 'red-jacket', name: 'Red Jacket', category: 'Outerwear', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#a8392f', shape: 'top' },
  { id: 'pink-blouse', name: 'Pink Blouse', category: 'Tops', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👚', tone: '#d39fa5', shape: 'blouse' },
  { id: 'wide-leg-jeans', name: 'Wide-Leg Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#5a7f9f', shape: 'pants' },
  { id: 'grey-coat', name: 'Grey Coat', category: 'Outerwear', colour: 'Grey', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#7d7e80', shape: 'top' },
  { id: 'red-heels', name: 'Red Heels', category: 'Shoes', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👟', tone: '#a3423c', shape: 'shoe' },
  { id: 'black-sneakers', name: 'Black Sneakers', category: 'Shoes', colour: 'Black', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#302f33', shape: 'shoe' },
  { id: 'red-trousers', name: 'Red Trousers', category: 'Bottoms', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👖', tone: '#a83a35', shape: 'pants' },
  { id: 'straight-jeans', name: 'Straight Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#638aaa', shape: 'pants' },
  { id: 'lilac-sweater', name: 'Lilac Sweater', category: 'Tops', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#b9a3cf', shape: 'top' },
  { id: 'grey-cardigan', name: 'Grey Cardigan', category: 'Outerwear', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#9a9b9d', shape: 'top' },
  { id: 'blue-sneakers', name: 'Blue Sneakers', category: 'Shoes', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👟', tone: '#4f74a8', shape: 'shoe' },
  { id: 'purple-skirt', name: 'Purple Skirt', category: 'Bottoms', colour: 'Purple', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#7e5aa3', shape: 'skirt' },
  { id: 'black-jeans', name: 'Black Jeans', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#2e2d31', shape: 'pants' },
  { id: 'navy-sweater', name: 'Navy Sweater', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#2f3e54', shape: 'top' },
  { id: 'black-boots', name: 'Black Boots', category: 'Shoes', colour: 'Black', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#474240', shape: 'shoe' },
  { id: 'navy-trousers', name: 'Navy Trousers', category: 'Bottoms', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#3f5266', shape: 'pants' },
  { id: 'khaki-shorts', name: 'Khaki Shorts', category: 'Bottoms', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', emoji: '🩳', tone: '#ad9270', shape: 'shorts' },
  { id: 'yellow-tee', name: 'Yellow Tee', category: 'Tops', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#e8c547', shape: 'top' },
  { id: 'grey-knit-dress', name: 'Grey Knit Dress', category: 'Dresses', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#8b8b8d', shape: 'dress' },
  { id: 'white-pants', name: 'White Pants', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👖', tone: '#d8d6d0', shape: 'pants' },
  { id: 'red-midi-skirt', name: 'Red Midi Skirt', category: 'Bottoms', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#9f3f3a', shape: 'skirt' },
  { id: 'sweatpants', name: 'Sweatpants', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#8a8a8a', shape: 'pants' },
  { id: 'beige-coat', name: 'Beige Coat', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#b19d85', shape: 'top' },
  { id: 'purple-joggers', name: 'Purple Joggers', category: 'Bottoms', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👖', tone: '#6d4c8f', shape: 'pants' },
  { id: 'yellow-skirt', name: 'Yellow Skirt', category: 'Bottoms', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#e9c54f', shape: 'skirt' },
  { id: 'black-dress', name: 'Black Dress', category: 'Dresses', colour: 'Black', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#343339', shape: 'dress' },
  { id: 'black-turtleneck', name: 'Black Turtleneck', category: 'Tops', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', emoji: '👕', tone: '#29282d', shape: 'top' },
  { id: 'green-maxi-dress', name: 'Green Maxi Dress', category: 'Dresses', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#4f7a52', shape: 'dress' },
  { id: 'black-leggings', name: 'Black Leggings', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '👖', tone: '#232226', shape: 'pants' },
  { id: 'white-cardigan', name: 'White Cardigan', category: 'Outerwear', colour: 'White', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#ecebe6', shape: 'top' },
  { id: 'black-puffer', name: 'Black Puffer', category: 'Outerwear', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#28272b', shape: 'top' },
  { id: 'rain-boots', name: 'Rain Boots', category: 'Shoes', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#3a393e', shape: 'shoe' },
  { id: 'grey-polo', name: 'Grey Polo', category: 'Tops', colour: 'Grey', occasion: 'Formal', weather: 'Sunny', emoji: '👕', tone: '#a7a8aa', shape: 'top' },
  { id: 'light-wash-jeans', name: 'Light Wash Jeans', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#9cb6cc', shape: 'pants' },
  { id: 'silk-blouse', name: 'Silk Blouse', category: 'Tops', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👚', tone: '#82956f', shape: 'blouse' },
  { id: 'ruffled-skirt', name: 'Ruffled Skirt', category: 'Bottoms', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#a0af87', shape: 'skirt' },
  { id: 'green-shorts', name: 'Green Shorts', category: 'Bottoms', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#5f8f5a', shape: 'shorts' },
  { id: 'white-skirt', name: 'White Skirt', category: 'Bottoms', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#ecebe6', shape: 'skirt' },
  { id: 'tan-sandals', name: 'Tan Sandals', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#b08a62', shape: 'shoe' },
  { id: 'purple-flats', name: 'Purple Flats', category: 'Shoes', colour: 'Purple', occasion: 'Formal', weather: 'Sunny', emoji: '👟', tone: '#6f4c94', shape: 'shoe' },
  { id: 'purple-fleece', name: 'Purple Fleece', category: 'Outerwear', colour: 'Purple', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#7a5a9e', shape: 'top' },
  { id: 'pink-skirt', name: 'Pink Skirt', category: 'Bottoms', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#d8a3aa', shape: 'skirt' },
  { id: 'red-blouse', name: 'Red Blouse', category: 'Tops', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👚', tone: '#b0403a', shape: 'blouse' },
  { id: 'navy-dress', name: 'Navy Dress', category: 'Dresses', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#2f3f56', shape: 'dress' },
  { id: 'green-sneakers', name: 'Green Sneakers', category: 'Shoes', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👟', tone: '#4f8a52', shape: 'shoe' },
  { id: 'cream-knit', name: 'Cream Knit', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#ddd0b8', shape: 'top' },
  { id: 'white-shorts', name: 'White Shorts', category: 'Bottoms', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#ecebe6', shape: 'shorts' },
  { id: 'black-tank-top', name: 'Black Tank Top', category: 'Tops', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#2f2e33', shape: 'top' },
  { id: 'grey-trousers', name: 'Grey Trousers', category: 'Bottoms', colour: 'Grey', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#7b7c7e', shape: 'pants' },
  { id: 'grey-tee', name: 'Grey Tee', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#9a9a98', shape: 'top' },
  { id: 'pink-sandals', name: 'Pink Sandals', category: 'Shoes', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👟', tone: '#dcaab0', shape: 'shoe' },
  { id: 'brown-pants', name: 'Brown Pants', category: 'Bottoms', colour: 'Brown', occasion: 'Formal', weather: 'Sunny', emoji: '👖', tone: '#665047', shape: 'pants' },
  { id: 'blue-wrap-dress', name: 'Blue Wrap Dress', category: 'Dresses', colour: 'Blue', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#4f74a8', shape: 'dress' },
  { id: 'brown-leather-jacket', name: 'Brown Leather Jacket', category: 'Outerwear', colour: 'Brown', occasion: 'Party', weather: 'Cloudy', emoji: '🧥', tone: '#5f3d2b', shape: 'top' },
  { id: 'beige-shirt-dress', name: 'Beige Shirt Dress', category: 'Dresses', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#cfb995', shape: 'dress' },
  { id: 'yellow-shorts', name: 'Yellow Shorts', category: 'Bottoms', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#edd060', shape: 'shorts' },
  { id: 'beige-chinos', name: 'Beige Chinos', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#d6c4a2', shape: 'pants' },
  { id: 'white-shirt', name: 'White Shirt', category: 'Tops', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👔', tone: '#dadbd5', shape: 'top' },
  { id: 'navy-raincoat', name: 'Navy Raincoat', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#2f3f56', shape: 'top' },
  { id: 'trench-coat', name: 'Trench Coat', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#c4a983', shape: 'top' },
  { id: 'purple-dress', name: 'Purple Dress', category: 'Dresses', colour: 'Purple', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#6f4c94', shape: 'dress' },
  { id: 'grey-running-shoes', name: 'Grey Running Shoes', category: 'Shoes', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#6b6c6f', shape: 'shoe' },
  { id: 'yellow-blouse', name: 'Yellow Blouse', category: 'Tops', colour: 'Yellow', occasion: 'Party', weather: 'Sunny', emoji: '👚', tone: '#f0d36a', shape: 'blouse' },
  { id: 'pink-slip-dress', name: 'Pink Slip Dress', category: 'Dresses', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#e6b3bb', shape: 'dress' },
  { id: 'yellow-raincoat', name: 'Yellow Raincoat', category: 'Outerwear', colour: 'Yellow', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#e8c03f', shape: 'top' },
  { id: 'white-sundress', name: 'White Sundress', category: 'Dresses', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#ecebe6', shape: 'dress' },
  { id: 'black-blazer', name: 'Black Blazer', category: 'Outerwear', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#2d2c31', shape: 'top' },
  { id: 'beige-linen-shirt', name: 'Beige Linen Shirt', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#cbb99a', shape: 'top' },
  { id: 'white-sneakers', name: 'White Sneakers', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👟', tone: '#e1e1d9', shape: 'shoe' },
  { id: 'brown-cami', name: 'Brown Cami', category: 'Tops', colour: 'Brown', occasion: 'Party', weather: 'Sunny', emoji: '👚', tone: '#80513f', shape: 'blouse' },
  { id: 'pink-tank-top', name: 'Pink Tank Top', category: 'Tops', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#e0b3b8', shape: 'top' },
  { id: 'brown-loafers', name: 'Brown Loafers', category: 'Shoes', colour: 'Brown', occasion: 'Formal', weather: 'Sunny', emoji: '👟', tone: '#5b3b2a', shape: 'shoe' },
  { id: 'blue-satin-blouse', name: 'Blue Satin Blouse', category: 'Tops', colour: 'Blue', occasion: 'Formal', weather: 'Sunny', emoji: '👚', tone: '#5b7fb0', shape: 'blouse' },
  { id: 'yellow-sundress', name: 'Yellow Sundress', category: 'Dresses', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#ecd062', shape: 'dress' }
]
const targets = ['silk-blouse', 'brown-pants', 'white-sneakers'].map(id => wardrobe.find(item => item.id === id))
const params = new URLSearchParams(window.location.search)
const initialVersion = ['A', 'B'].includes(params.get('version')?.toUpperCase()) ? params.get('version').toUpperCase() : ''
const version = ref(initialVersion)
const participant = ref('')
const phase = ref('setup')
const query = ref('')
const category = ref('All Items')
const filtersOpen = ref(false)
const selectedTags = ref({ Occasion: [], Weather: [], Colours: [] })
const collected = ref([])
const startedAt = ref(0)
const finishedAt = ref(0)
const elapsed = ref(0)
const actions = ref([])
const lastAction = ref('')
const selectedItem = ref(null)
let intervalId
const categories = ['All Items', 'Tops', 'Bottoms', 'Dresses', 'Outerwear', 'Shoes']
const tagGroups = { Occasion: ['Formal', 'Casual', 'Party'], Weather: ['Sunny', 'Rainy', 'Cloudy'], Colours: ['Green', 'Brown', 'White', 'Black', 'Grey', 'Beige', 'Blue', 'Pink', 'Red', 'Yellow', 'Purple'] }
const searchTerms = (s) => s.toLowerCase().trim().split(/\s+/).filter(Boolean)
const visible = computed(() => {
  if (version.value === 'B') {
    const words = searchTerms(query.value)
    return wardrobe.filter(item => words.every(word => `${item.name} ${item.category} ${item.colour} ${item.occasion} ${item.weather}`.toLowerCase().includes(word)))
  }
  return wardrobe.filter(item => {
    if (category.value !== 'All Items' && item.category !== category.value) return false
    return Object.entries(selectedTags.value).every(([kind, values]) => !values.length || values.includes(kind === 'Colours' ? item.colour : item[kind === 'Occasion' ? 'occasion' : 'weather']))
  })
})
const inCategory = computed(() => version.value === 'A' && category.value !== 'All Items')
const activeFilterCount = computed(() => Object.values(selectedTags.value).flat().length)
const foundCount = computed(() => targets.filter(t => collected.value.includes(t.id)).length)
const navItems = [{ label: 'Home', icon: 'home' }, { label: 'Wardrobe', icon: 'wardrobe' }, { label: 'Fitting Room', icon: 'hanger' }, { label: 'WearTogether', icon: 'people' }]
// Fixed placeholder details so every item page has the same layout as the app
const itemStats = (item) => {
  const n = wardrobe.findIndex(i => i.id === item.id)
  return { outfits: (n * 7) % 19 + 3, lastAdded: (n * 5) % 13 + 1 }
}
const complete = computed(() => targets.every(t => collected.value.includes(t.id)))
const seconds = computed(() => Math.round((finishedAt.value || elapsed.value) / 100) / 10)
function record(type, detail = '') {
  if (phase.value !== 'test') return
  actions.value.push({ seconds: Math.round((performance.now() - startedAt.value) / 100) / 10, type, detail })
  lastAction.value = type
}
function start() {
  if (!version.value) return
  category.value = 'All Items'; query.value = ''; collected.value = []; filtersOpen.value = false
  selectedTags.value = { Occasion: [], Weather: [], Colours: [] }
  actions.value = []; selectedItem.value = null; finishedAt.value = 0; elapsed.value = 0
  phase.value = 'test'
  startedAt.value = performance.now()
  intervalId = setInterval(() => { elapsed.value = performance.now() - startedAt.value }, 100)
}
function stop() {
  if (intervalId) clearInterval(intervalId)
  finishedAt.value = performance.now() - startedAt.value
  phase.value = 'done'
}
function openFilters() { filtersOpen.value = true; record('toggle_filter_panel', 'open') }
function closeFilters() { filtersOpen.value = false; record('toggle_filter_panel', 'closed') }
function applyFilters() { filtersOpen.value = false; record('apply_filters') }
function setCategory(next) { category.value = next; record('select_category', next) }
function toggleTag(kind, value) {
  const arr = [...selectedTags.value[kind]]
  const index = arr.indexOf(value)
  if (index >= 0) arr.splice(index, 1); else arr.push(value)
  selectedTags.value = { ...selectedTags.value, [kind]: arr }
  record('toggle_filter', `${kind}: ${value}`)
}
function clearFilters() { selectedTags.value = { Occasion: [], Weather: [], Colours: [] }; record('clear_filters') }
function openItem(item) { selectedItem.value = item; record('open_item', item.name) }
function addItem() {
  const item = selectedItem.value
  if (!item) return
  if (!collected.value.includes(item.id)) collected.value = [...collected.value, item.id]
  record('select_item', item.name)
  selectedItem.value = null
  if (complete.value) stop()
}
watch(query, newValue => { record('search_query_change', newValue) })
onUnmounted(() => { if (intervalId) clearInterval(intervalId) })
function csvEscape(value) { return `"${String(value ?? '').replaceAll('"', '""')}"` }
function exportCsv() {
  const summary = {
    participant: participant.value || 'anonymous', version: version.value,
    completed: complete.value, duration_seconds: seconds.value,
    total_interactions: actions.value.filter(a => a.type !== 'search_query_change').length,
    search_edits: actions.value.filter(a => a.type === 'search_query_change').length,
    selected_items: collected.value.map(id => wardrobe.find(i => i.id === id)?.name).join(' | '),
    event_log_json: JSON.stringify(actions.value)
  }
  const csv = Object.keys(summary).join(',') + '\n' + Object.values(summary).map(csvEscape).join(',') + '\n'
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8' })
  const url = URL.createObjectURL(blob)
  const anchor = document.createElement('a')
  anchor.href = url; anchor.download = `wearabouts-${version.value}-${(participant.value || 'anonymous').replace(/[^a-zA-Z0-9_-]/g, '_')}.csv`
  anchor.click(); URL.revokeObjectURL(url)
}
</script>

<template>
  <div class="app-shell">
    <div class="study-header"><span class="study-kicker">ITER 2.5 · USABILITY STUDY</span><span class="study-subtitle">Wearabouts · Wardrobe discovery</span></div>
    <div v-if="phase !== 'done'" class="study-layout" :class="{ 'setup-layout': phase === 'setup' }">
    <section v-if="phase === 'setup'" class="intro panel">
      <div class="logo">Wearabouts<span class="logo-dot">.</span></div>
      <div class="eyebrow">WARDROBE FINDABILITY STUDY</div>
      <h1>Find your outfit, your way.</h1>
      <p>You are heading to dinner with friends. Find the three pieces shown in the reference images and add them to your outfit.</p>
      <label class="field-label" for="participant">Participant code (optional)</label>
      <input id="participant" v-model="participant" placeholder="e.g. P01" autocomplete="off" />
      <div v-if="!initialVersion" class="version-picker">
        <div class="field-label">Researcher: choose the assigned version</div>
        <button class="version-choice" :class="{ chosen: version === 'A' }" @click="version = 'A'">A · Category navigation + tag filters</button>
        <button class="version-choice" :class="{ chosen: version === 'B' }" @click="version = 'B'">B · Free-text keyword search</button>
      </div>
      <div v-else class="version-note">Your assigned study interface is ready.</div>
      <button class="primary wide" :disabled="!version" @click="start">Start task <span>→</span></button>
      <p class="fine-print">The timer begins when you press Start. Select each clothing item to add it to your outfit. This demo stores no results on a server; the researcher can export a CSV afterward.</p>
    </section>

    <div v-else-if="phase === 'test'" class="phone">
      <header class="phone-top">
        <span>9:41</span>
        <svg class="status-icons" viewBox="0 0 60 14" aria-hidden="true"><g fill="currentColor"><rect x="0" y="9" width="3" height="4" rx=".7" /><rect x="4.5" y="6.5" width="3" height="6.5" rx=".7" /><rect x="9" y="4" width="3" height="9" rx=".7" /><rect x="13.5" y="1.5" width="3" height="11.5" rx=".7" /><path d="M29 12.5 26.6 10a3.4 3.4 0 0 1 4.8 0zM24.6 8a6.2 6.2 0 0 1 8.8 0l1.4-1.4a8.2 8.2 0 0 0-11.6 0z" /><rect x="40" y="2.5" width="16" height="9" rx="2.4" fill="none" stroke="currentColor" stroke-width="1.1" opacity=".5" /><rect x="41.6" y="4.1" width="12.8" height="5.8" rx="1.3" /><path d="M57.3 5.5v3a1.6 1.6 0 0 0 0-3z" opacity=".5" /></g></svg>
      </header>

      <div class="phone-scroll">
        <div class="page-head">
          <button v-if="inCategory" class="circle-btn" aria-label="Back to all items" @click="setCategory('All Items')"><AppIcon name="back" /></button>
          <div class="page-title">
            <h1>{{ inCategory ? category : 'Wardrobe' }}</h1>
            <span>{{ inCategory ? `${visible.length} Items` : `Total ${visible.length} items` }}</span>
          </div>
          <div class="head-actions">
            <button v-if="version === 'A'" class="circle-btn" aria-label="Filter" @click="openFilters"><AppIcon name="filter" /><span v-if="activeFilterCount" class="badge">{{ activeFilterCount }}</span></button>
            <span class="circle-btn" aria-hidden="true"><AppIcon name="basket" /><span v-if="collected.length" class="badge">{{ collected.length }}</span></span>
            <span class="circle-btn" aria-hidden="true"><AppIcon name="plus" /></span>
          </div>
        </div>

        <div class="task-strip"><span>Dinner outfit · find the pieces in the reference images</span><strong>{{ foundCount }}/3</strong></div>

        <div v-if="version === 'A'" class="tabs"><button v-for="cat in categories" :key="cat" :class="{ active: category === cat }" @click="setCategory(cat)">{{ cat }}</button></div>
        <template v-else>
          <div class="search-wrap"><AppIcon name="search" /><input v-model="query" aria-label="Search your wardrobe" type="search" placeholder="Search clothing, colour or tag..." autocomplete="off" /></div>
          <div class="search-hint">Search by name, colour, occasion or weather</div>
        </template>

        <div class="item-grid" :class="{ 'two-col': inCategory }">
          <button v-for="item in visible" :key="item.id" class="item-card" @click="openItem(item)">
            <ClothingImage :item="item" />
            <div class="item-title">{{ item.name }}</div>
            <div class="item-meta">{{ inCategory ? `${item.occasion} • ${item.colour}` : item.category }}</div>
            <span v-if="collected.includes(item.id)" class="item-added">✓ Added</span>
          </button>
        </div>
        <p v-if="visible.length === 0" class="empty">No matching items. Try a different {{ version === 'A' ? 'filter' : 'search' }}.</p>
      </div>

      <nav class="bottom-nav" aria-hidden="true">
        <span v-for="nav in navItems" :key="nav.label" :class="{ 'nav-current': nav.label === 'Wardrobe' }"><span class="nav-icon"><AppIcon :name="nav.icon" /></span><small>{{ nav.label }}</small></span>
      </nav>

      <div v-if="filtersOpen" class="screen">
        <div class="screen-head"><button class="circle-btn" aria-label="Back" @click="closeFilters"><AppIcon name="back" /></button><h1>Filter</h1></div>
        <div class="screen-body">
          <div v-for="(options, kind, index) in tagGroups" :key="kind" class="filter-group">
            <div class="filter-group-head"><h2>{{ kind }}</h2><button v-if="index === 0" class="text-btn" @click="clearFilters">Clear Selection</button></div>
            <div class="chip-row"><button v-for="tag in options" :key="tag" class="chip" :class="{ selected: selectedTags[kind].includes(tag) }" @click="toggleTag(kind, tag)">{{ tag }}</button></div>
          </div>
          <div class="filter-actions">
            <button class="pill-primary" @click="applyFilters">Apply</button>
            <button class="pill-outline" @click="closeFilters">Back To Wardrobe</button>
          </div>
        </div>
      </div>

      <div v-if="selectedItem" class="screen">
        <div class="screen-head"><button class="circle-btn" aria-label="Close item details" @click="selectedItem = null"><AppIcon name="back" /></button><h1>Item details</h1></div>
        <div class="screen-body">
          <div class="detail-image"><ClothingImage :item="selectedItem" /></div>
          <div class="detail-name"><h2>{{ selectedItem.name }}</h2><span>{{ selectedItem.category }}</span></div>
          <div class="chip-row detail-tags"><span class="chip">{{ selectedItem.occasion }}</span><span class="chip">{{ selectedItem.colour }}</span><span class="chip">{{ selectedItem.weather }}</span></div>
          <div class="detail-row"><AppIcon name="layers" /><span>Saved outfits</span><strong>{{ itemStats(selectedItem).outfits }} outfits</strong></div>
          <div class="detail-row"><AppIcon name="basket" /><span>Last added to basket</span><strong>{{ itemStats(selectedItem).lastAdded }} days ago</strong></div>
          <div class="detail-row"><AppIcon name="archive" /><span>Location</span><strong>Wardrobe</strong></div>
          <div class="ai-note"><AppIcon name="sparkle" /><div><small>AI STYLING NOTE</small><p>Works well for {{ selectedItem.occasion.toLowerCase() }} looks on {{ selectedItem.weather.toLowerCase() }} days</p></div></div>
        </div>
        <div class="detail-actions">
          <button class="pill-outline" @click="selectedItem = null">Back</button>
          <button class="pill-primary" :disabled="collected.includes(selectedItem.id)" @click="addItem"><AppIcon name="basket" />{{ collected.includes(selectedItem.id) ? 'Added to Outfit' : 'Add to Outfit' }}</button>
        </div>
      </div>
    </div>

    <aside class="reference-panel" aria-labelledby="reference-heading">
      <h2 id="reference-heading">Find these pieces</h2>
      <p>Match the pictures to items in your wardrobe.</p>
      <div class="reference-grid">
        <div v-for="(item, index) in targets" :key="item.id" class="reference-card" :class="{ found: collected.includes(item.id) }">
          <ClothingImage :item="item" role="img" :aria-label="`Reference item ${index + 1}`" />
          <span v-if="collected.includes(item.id)" class="reference-found"><span aria-hidden="true">✓ </span>Found</span>
        </div>
      </div>
    </aside>
    </div>

    <section v-else class="intro panel done-panel"><div class="success-icon">✓</div><div class="logo">Wearabouts<span class="logo-dot">.</span></div><h1>Outfit complete!</h1><p>You found all three pieces. Thank you for taking part.</p><div class="stats"><div><strong>{{ seconds.toFixed(1) }}s</strong><span>Completion time</span></div><div><strong>{{ actions.filter(a => a.type !== 'search_query_change').length }}</strong><span>Non-typing interactions</span></div></div><p class="fine-print">Researcher: export this session's data. Note that keyboard input is recorded as query-change events, not individual keystroke counts.</p><button class="primary wide" @click="exportCsv">Download session CSV ↓</button><button class="secondary wide" @click="phase = 'setup'">New participant</button></section>
  </div>
</template>
