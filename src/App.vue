<script setup>
import { ref, computed, watch, onUnmounted } from 'vue'
import ClothingImage from './components/ClothingImage.vue'
import AppIcon from './components/AppIcon.vue'

const wardrobe = [
  { id: 'white-coat', name: 'White Coat', category: 'Outerwear', colour: 'White', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#e6e5df', shape: 'coat' },
  { id: 'red-sneakers', name: 'Red Sneakers', category: 'Shoes', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#c0392f', shape: 'shoe' },
  { id: 'black-coat', name: 'Black Coat', category: 'Outerwear', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#2b2a2f', shape: 'coat' },
  { id: 'pink-tee', name: 'Pink Tee', category: 'Tops', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#eba3b8', shape: 'top' },
  { id: 'yellow-coat', name: 'Yellow Coat', category: 'Outerwear', colour: 'Yellow', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#f0c93a', shape: 'coat' },
  { id: 'blue-pants', name: 'Blue Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#4a72b0', shape: 'pants' },
  { id: 'pink-boots', name: 'Pink Boots', category: 'Shoes', colour: 'Pink', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#eba3b8', shape: 'boot' },
  { id: 'pink-heels', name: 'Pink Heels', category: 'Shoes', colour: 'Pink', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#eba3b8', shape: 'heel' },
  { id: 'orange-tee', name: 'Orange Tee', category: 'Tops', colour: 'Orange', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#e87a2e', shape: 'top' },
  { id: 'pink-coat', name: 'Pink Coat', category: 'Outerwear', colour: 'Pink', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#eba3b8', shape: 'coat' },
  { id: 'green-mini-skirt', name: 'Green Mini Skirt', category: 'Bottoms', colour: 'Green', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#5c9a5b', shape: 'miniskirt' },
  { id: 'red-heels', name: 'Red Heels', category: 'Shoes', colour: 'Red', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#c0392f', shape: 'heel' },
  { id: 'black-mini-skirt', name: 'Black Mini Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#2b2a2f', shape: 'miniskirt' },
  { id: 'beige-tank-top', name: 'Beige Tank Top', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#c9a774', shape: 'tank' },
  { id: 'blue-maxi-dress', name: 'Blue Maxi Dress', category: 'Dresses', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#4a72b0', shape: 'longdress' },
  { id: 'grey-tee', name: 'Grey Tee', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#8e8f92', shape: 'top' },
  { id: 'black-skirt', name: 'Black Skirt', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#2b2a2f', shape: 'skirt' },
  { id: 'brown-skirt', name: 'Brown Skirt', category: 'Bottoms', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#6b4a36', shape: 'skirt' },
  { id: 'grey-wide-leg-pants', name: 'Grey Wide-Leg Pants', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#8e8f92', shape: 'widepants' },
  { id: 'pink-jacket', name: 'Pink Jacket', category: 'Outerwear', colour: 'Pink', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#eba3b8', shape: 'jacket' },
  { id: 'orange-dress', name: 'Orange Dress', category: 'Dresses', colour: 'Orange', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#e87a2e', shape: 'dress' },
  { id: 'yellow-hoodie', name: 'Yellow Hoodie', category: 'Tops', colour: 'Yellow', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#f0c93a', shape: 'hoodie' },
  { id: 'beige-boots', name: 'Beige Boots', category: 'Shoes', colour: 'Beige', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#c9a774', shape: 'boot' },
  { id: 'white-tee', name: 'White Tee', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#e6e5df', shape: 'top' },
  { id: 'pink-pants', name: 'Pink Pants', category: 'Bottoms', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#eba3b8', shape: 'pants' },
  { id: 'black-jacket', name: 'Black Jacket', category: 'Outerwear', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#2b2a2f', shape: 'jacket' },
  { id: 'black-hoodie', name: 'Black Hoodie', category: 'Tops', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#2b2a2f', shape: 'hoodie' },
  { id: 'blue-heels', name: 'Blue Heels', category: 'Shoes', colour: 'Blue', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#4a72b0', shape: 'heel' },
  { id: 'grey-skirt', name: 'Grey Skirt', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#8e8f92', shape: 'skirt' },
  { id: 'beige-wide-leg-pants', name: 'Beige Wide-Leg Pants', category: 'Bottoms', colour: 'Beige', occasion: 'Party', weather: 'Cloudy', emoji: '👖', tone: '#c9a774', shape: 'widepants' },
  { id: 'brown-jacket', name: 'Brown Jacket', category: 'Outerwear', colour: 'Brown', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#6b4a36', shape: 'jacket' },
  { id: 'yellow-wide-leg-pants', name: 'Yellow Wide-Leg Pants', category: 'Bottoms', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#f0c93a', shape: 'widepants' },
  { id: 'grey-jacket', name: 'Grey Jacket', category: 'Outerwear', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#8e8f92', shape: 'jacket' },
  { id: 'white-tank-top', name: 'White Tank Top', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#e6e5df', shape: 'tank' },
  { id: 'red-jacket', name: 'Red Jacket', category: 'Outerwear', colour: 'Red', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#c0392f', shape: 'jacket' },
  { id: 'white-maxi-dress', name: 'White Maxi Dress', category: 'Dresses', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#e6e5df', shape: 'longdress' },
  { id: 'purple-tee', name: 'Purple Tee', category: 'Tops', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#7d55a8', shape: 'top' },
  { id: 'red-hoodie', name: 'Red Hoodie', category: 'Tops', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#c0392f', shape: 'hoodie' },
  { id: 'black-boots', name: 'Black Boots', category: 'Shoes', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#2b2a2f', shape: 'boot' },
  { id: 'red-tee', name: 'Red Tee', category: 'Tops', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#c0392f', shape: 'top' },
  { id: 'yellow-tank-top', name: 'Yellow Tank Top', category: 'Tops', colour: 'Yellow', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#f0c93a', shape: 'tank' },
  { id: 'brown-sneakers', name: 'Brown Sneakers', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#6b4a36', shape: 'shoe' },
  { id: 'brown-shorts', name: 'Brown Shorts', category: 'Bottoms', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#6b4a36', shape: 'shorts' },
  { id: 'black-maxi-dress', name: 'Black Maxi Dress', category: 'Dresses', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#2b2a2f', shape: 'longdress' },
  { id: 'white-dress', name: 'White Dress', category: 'Dresses', colour: 'White', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#e6e5df', shape: 'dress' },
  { id: 'black-tank-top', name: 'Black Tank Top', category: 'Tops', colour: 'Black', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#2b2a2f', shape: 'tank' },
  { id: 'yellow-dress', name: 'Yellow Dress', category: 'Dresses', colour: 'Yellow', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#f0c93a', shape: 'dress' },
  { id: 'beige-jacket', name: 'Beige Jacket', category: 'Outerwear', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#c9a774', shape: 'jacket' },
  { id: 'brown-dress', name: 'Brown Dress', category: 'Dresses', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#6b4a36', shape: 'dress' },
  { id: 'grey-mini-skirt', name: 'Grey Mini Skirt', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#8e8f92', shape: 'miniskirt' },
  { id: 'red-pants', name: 'Red Pants', category: 'Bottoms', colour: 'Red', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#c0392f', shape: 'pants' },
  { id: 'beige-shorts', name: 'Beige Shorts', category: 'Bottoms', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#c9a774', shape: 'shorts' },
  { id: 'green-blouse', name: 'Green Blouse', category: 'Tops', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👚', tone: '#5c9a5b', shape: 'blouse' },
  { id: 'purple-dress', name: 'Purple Dress', category: 'Dresses', colour: 'Purple', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#7d55a8', shape: 'dress' },
  { id: 'red-wide-leg-pants', name: 'Red Wide-Leg Pants', category: 'Bottoms', colour: 'Red', occasion: 'Party', weather: 'Cloudy', emoji: '👖', tone: '#c0392f', shape: 'widepants' },
  { id: 'yellow-skirt', name: 'Yellow Skirt', category: 'Bottoms', colour: 'Yellow', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#f0c93a', shape: 'skirt' },
  { id: 'yellow-boots', name: 'Yellow Boots', category: 'Shoes', colour: 'Yellow', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#f0c93a', shape: 'boot' },
  { id: 'yellow-shorts', name: 'Yellow Shorts', category: 'Bottoms', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#f0c93a', shape: 'shorts' },
  { id: 'green-wide-leg-pants', name: 'Green Wide-Leg Pants', category: 'Bottoms', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#5c9a5b', shape: 'widepants' },
  { id: 'orange-tank-top', name: 'Orange Tank Top', category: 'Tops', colour: 'Orange', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#e87a2e', shape: 'tank' },
  { id: 'grey-hoodie', name: 'Grey Hoodie', category: 'Tops', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#8e8f92', shape: 'hoodie' },
  { id: 'purple-mini-skirt', name: 'Purple Mini Skirt', category: 'Bottoms', colour: 'Purple', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#7d55a8', shape: 'miniskirt' },
  { id: 'black-sandals', name: 'Black Sandals', category: 'Shoes', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#2b2a2f', shape: 'sandal' },
  { id: 'pink-mini-skirt', name: 'Pink Mini Skirt', category: 'Bottoms', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#eba3b8', shape: 'miniskirt' },
  { id: 'grey-shorts', name: 'Grey Shorts', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#8e8f92', shape: 'shorts' },
  { id: 'white-hoodie', name: 'White Hoodie', category: 'Tops', colour: 'White', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#e6e5df', shape: 'hoodie' },
  { id: 'green-coat', name: 'Green Coat', category: 'Outerwear', colour: 'Green', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#5c9a5b', shape: 'coat' },
  { id: 'red-coat', name: 'Red Coat', category: 'Outerwear', colour: 'Red', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#c0392f', shape: 'coat' },
  { id: 'black-heels', name: 'Black Heels', category: 'Shoes', colour: 'Black', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#2b2a2f', shape: 'heel' },
  { id: 'beige-hoodie', name: 'Beige Hoodie', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#c9a774', shape: 'hoodie' },
  { id: 'red-tank-top', name: 'Red Tank Top', category: 'Tops', colour: 'Red', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#c0392f', shape: 'tank' },
  { id: 'grey-coat', name: 'Grey Coat', category: 'Outerwear', colour: 'Grey', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#8e8f92', shape: 'coat' },
  { id: 'beige-tee', name: 'Beige Tee', category: 'Tops', colour: 'Beige', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#c9a774', shape: 'top' },
  { id: 'yellow-sneakers', name: 'Yellow Sneakers', category: 'Shoes', colour: 'Yellow', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#f0c93a', shape: 'shoe' },
  { id: 'blue-boots', name: 'Blue Boots', category: 'Shoes', colour: 'Blue', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#4a72b0', shape: 'boot' },
  { id: 'orange-mini-skirt', name: 'Orange Mini Skirt', category: 'Bottoms', colour: 'Orange', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#e87a2e', shape: 'miniskirt' },
  { id: 'purple-boots', name: 'Purple Boots', category: 'Shoes', colour: 'Purple', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#7d55a8', shape: 'boot' },
  { id: 'purple-jacket', name: 'Purple Jacket', category: 'Outerwear', colour: 'Purple', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#7d55a8', shape: 'jacket' },
  { id: 'pink-skirt', name: 'Pink Skirt', category: 'Bottoms', colour: 'Pink', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#eba3b8', shape: 'skirt' },
  { id: 'brown-trousers', name: 'Brown Trousers', category: 'Bottoms', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#6b4a36', shape: 'pants' },
  { id: 'green-sneakers', name: 'Green Sneakers', category: 'Shoes', colour: 'Green', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#5c9a5b', shape: 'shoe' },
  { id: 'green-sandals', name: 'Green Sandals', category: 'Shoes', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#5c9a5b', shape: 'sandal' },
  { id: 'orange-shorts', name: 'Orange Shorts', category: 'Bottoms', colour: 'Orange', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#e87a2e', shape: 'shorts' },
  { id: 'purple-coat', name: 'Purple Coat', category: 'Outerwear', colour: 'Purple', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#7d55a8', shape: 'coat' },
  { id: 'red-sandals', name: 'Red Sandals', category: 'Shoes', colour: 'Red', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#c0392f', shape: 'sandal' },
  { id: 'purple-wide-leg-pants', name: 'Purple Wide-Leg Pants', category: 'Bottoms', colour: 'Purple', occasion: 'Party', weather: 'Cloudy', emoji: '👖', tone: '#7d55a8', shape: 'widepants' },
  { id: 'brown-tank-top', name: 'Brown Tank Top', category: 'Tops', colour: 'Brown', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#6b4a36', shape: 'tank' },
  { id: 'yellow-heels', name: 'Yellow Heels', category: 'Shoes', colour: 'Yellow', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#f0c93a', shape: 'heel' },
  { id: 'black-sneakers', name: 'Black Sneakers', category: 'Shoes', colour: 'Black', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#2b2a2f', shape: 'shoe' },
  { id: 'red-dress', name: 'Red Dress', category: 'Dresses', colour: 'Red', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#c0392f', shape: 'dress' },
  { id: 'brown-maxi-dress', name: 'Brown Maxi Dress', category: 'Dresses', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#6b4a36', shape: 'longdress' },
  { id: 'green-dress', name: 'Green Dress', category: 'Dresses', colour: 'Green', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#5c9a5b', shape: 'dress' },
  { id: 'blue-hoodie', name: 'Blue Hoodie', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#4a72b0', shape: 'hoodie' },
  { id: 'grey-pants', name: 'Grey Pants', category: 'Bottoms', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#8e8f92', shape: 'pants' },
  { id: 'purple-shorts', name: 'Purple Shorts', category: 'Bottoms', colour: 'Purple', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#7d55a8', shape: 'shorts' },
  { id: 'black-wide-leg-pants', name: 'Black Wide-Leg Pants', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#2b2a2f', shape: 'widepants' },
  { id: 'pink-sandals', name: 'Pink Sandals', category: 'Shoes', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#eba3b8', shape: 'sandal' },
  { id: 'yellow-mini-skirt', name: 'Yellow Mini Skirt', category: 'Bottoms', colour: 'Yellow', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#f0c93a', shape: 'miniskirt' },
  { id: 'yellow-maxi-dress', name: 'Yellow Maxi Dress', category: 'Dresses', colour: 'Yellow', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#f0c93a', shape: 'longdress' },
  { id: 'pink-wide-leg-pants', name: 'Pink Wide-Leg Pants', category: 'Bottoms', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#eba3b8', shape: 'widepants' },
  { id: 'purple-sneakers', name: 'Purple Sneakers', category: 'Shoes', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#7d55a8', shape: 'shoe' },
  { id: 'orange-jacket', name: 'Orange Jacket', category: 'Outerwear', colour: 'Orange', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#e87a2e', shape: 'jacket' },
  { id: 'brown-tee', name: 'Brown Tee', category: 'Tops', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#6b4a36', shape: 'top' },
  { id: 'beige-sandals', name: 'Beige Sandals', category: 'Shoes', colour: 'Beige', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#c9a774', shape: 'sandal' },
  { id: 'red-maxi-dress', name: 'Red Maxi Dress', category: 'Dresses', colour: 'Red', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#c0392f', shape: 'longdress' },
  { id: 'white-heels', name: 'White Heels', category: 'Shoes', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#e6e5df', shape: 'heel' },
  { id: 'white-trainers', name: 'White Trainers', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#e6e5df', shape: 'shoe' },
  { id: 'pink-hoodie', name: 'Pink Hoodie', category: 'Tops', colour: 'Pink', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#eba3b8', shape: 'hoodie' },
  { id: 'white-boots', name: 'White Boots', category: 'Shoes', colour: 'White', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#e6e5df', shape: 'boot' },
  { id: 'grey-dress', name: 'Grey Dress', category: 'Dresses', colour: 'Grey', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#8e8f92', shape: 'dress' },
  { id: 'orange-skirt', name: 'Orange Skirt', category: 'Bottoms', colour: 'Orange', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#e87a2e', shape: 'skirt' },
  { id: 'white-jacket', name: 'White Jacket', category: 'Outerwear', colour: 'White', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#e6e5df', shape: 'jacket' },
  { id: 'yellow-jacket', name: 'Yellow Jacket', category: 'Outerwear', colour: 'Yellow', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#f0c93a', shape: 'jacket' },
  { id: 'orange-sandals', name: 'Orange Sandals', category: 'Shoes', colour: 'Orange', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#e87a2e', shape: 'sandal' },
  { id: 'yellow-tee', name: 'Yellow Tee', category: 'Tops', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#f0c93a', shape: 'top' },
  { id: 'green-skirt', name: 'Green Skirt', category: 'Bottoms', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#5c9a5b', shape: 'skirt' },
  { id: 'purple-maxi-dress', name: 'Purple Maxi Dress', category: 'Dresses', colour: 'Purple', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#7d55a8', shape: 'longdress' },
  { id: 'brown-mini-skirt', name: 'Brown Mini Skirt', category: 'Bottoms', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#6b4a36', shape: 'miniskirt' },
  { id: 'beige-mini-skirt', name: 'Beige Mini Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#c9a774', shape: 'miniskirt' },
  { id: 'grey-sandals', name: 'Grey Sandals', category: 'Shoes', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#8e8f92', shape: 'sandal' },
  { id: 'black-shorts', name: 'Black Shorts', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#2b2a2f', shape: 'shorts' },
  { id: 'green-shorts', name: 'Green Shorts', category: 'Bottoms', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#5c9a5b', shape: 'shorts' },
  { id: 'purple-heels', name: 'Purple Heels', category: 'Shoes', colour: 'Purple', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#7d55a8', shape: 'heel' },
  { id: 'beige-heels', name: 'Beige Heels', category: 'Shoes', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#c9a774', shape: 'heel' },
  { id: 'purple-tank-top', name: 'Purple Tank Top', category: 'Tops', colour: 'Purple', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#7d55a8', shape: 'tank' },
  { id: 'silk-blouse', name: 'Silk Blouse', category: 'Tops', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👚', tone: '#5c9a5b', shape: 'blouse' },
  { id: 'white-pants', name: 'White Pants', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#e6e5df', shape: 'pants' },
  { id: 'green-pants', name: 'Green Pants', category: 'Bottoms', colour: 'Green', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#5c9a5b', shape: 'pants' },
  { id: 'purple-hoodie', name: 'Purple Hoodie', category: 'Tops', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#7d55a8', shape: 'hoodie' },
  { id: 'brown-boots', name: 'Brown Boots', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#6b4a36', shape: 'boot' },
  { id: 'orange-pants', name: 'Orange Pants', category: 'Bottoms', colour: 'Orange', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#e87a2e', shape: 'pants' },
  { id: 'pink-maxi-dress', name: 'Pink Maxi Dress', category: 'Dresses', colour: 'Pink', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#eba3b8', shape: 'longdress' },
  { id: 'beige-skirt', name: 'Beige Skirt', category: 'Bottoms', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#c9a774', shape: 'skirt' },
  { id: 'grey-tank-top', name: 'Grey Tank Top', category: 'Tops', colour: 'Grey', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#8e8f92', shape: 'tank' },
  { id: 'purple-skirt', name: 'Purple Skirt', category: 'Bottoms', colour: 'Purple', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#7d55a8', shape: 'skirt' },
  { id: 'beige-sneakers', name: 'Beige Sneakers', category: 'Shoes', colour: 'Beige', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#c9a774', shape: 'shoe' },
  { id: 'white-shorts', name: 'White Shorts', category: 'Bottoms', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#e6e5df', shape: 'shorts' },
  { id: 'white-skirt', name: 'White Skirt', category: 'Bottoms', colour: 'White', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#e6e5df', shape: 'skirt' },
  { id: 'blue-wide-leg-pants', name: 'Blue Wide-Leg Pants', category: 'Bottoms', colour: 'Blue', occasion: 'Party', weather: 'Cloudy', emoji: '👖', tone: '#4a72b0', shape: 'widepants' },
  { id: 'beige-coat', name: 'Beige Coat', category: 'Outerwear', colour: 'Beige', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#c9a774', shape: 'coat' },
  { id: 'blue-skirt', name: 'Blue Skirt', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#4a72b0', shape: 'skirt' },
  { id: 'black-tee', name: 'Black Tee', category: 'Tops', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#2b2a2f', shape: 'top' },
  { id: 'beige-pants', name: 'Beige Pants', category: 'Bottoms', colour: 'Beige', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#c9a774', shape: 'pants' },
  { id: 'red-skirt', name: 'Red Skirt', category: 'Bottoms', colour: 'Red', occasion: 'Casual', weather: 'Cloudy', emoji: '👗', tone: '#c0392f', shape: 'skirt' },
  { id: 'brown-hoodie', name: 'Brown Hoodie', category: 'Tops', colour: 'Brown', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#6b4a36', shape: 'hoodie' },
  { id: 'grey-maxi-dress', name: 'Grey Maxi Dress', category: 'Dresses', colour: 'Grey', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#8e8f92', shape: 'longdress' },
  { id: 'blue-jacket', name: 'Blue Jacket', category: 'Outerwear', colour: 'Blue', occasion: 'Casual', weather: 'Rainy', emoji: '🧥', tone: '#4a72b0', shape: 'jacket' },
  { id: 'blue-dress', name: 'Blue Dress', category: 'Dresses', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#4a72b0', shape: 'dress' },
  { id: 'red-shorts', name: 'Red Shorts', category: 'Bottoms', colour: 'Red', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#c0392f', shape: 'shorts' },
  { id: 'pink-tank-top', name: 'Pink Tank Top', category: 'Tops', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👕', tone: '#eba3b8', shape: 'tank' },
  { id: 'brown-sandals', name: 'Brown Sandals', category: 'Shoes', colour: 'Brown', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#6b4a36', shape: 'sandal' },
  { id: 'blue-mini-skirt', name: 'Blue Mini Skirt', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#4a72b0', shape: 'miniskirt' },
  { id: 'pink-dress', name: 'Pink Dress', category: 'Dresses', colour: 'Pink', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#eba3b8', shape: 'dress' },
  { id: 'blue-tank-top', name: 'Blue Tank Top', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👕', tone: '#4a72b0', shape: 'tank' },
  { id: 'brown-pants', name: 'Brown Pants', category: 'Bottoms', colour: 'Brown', occasion: 'Formal', weather: 'Sunny', emoji: '👖', tone: '#6b4a36', shape: 'pants' },
  { id: 'white-sandals', name: 'White Sandals', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#e6e5df', shape: 'sandal' },
  { id: 'blue-coat', name: 'Blue Coat', category: 'Outerwear', colour: 'Blue', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#4a72b0', shape: 'coat' },
  { id: 'green-jacket', name: 'Green Jacket', category: 'Outerwear', colour: 'Green', occasion: 'Casual', weather: 'Cloudy', emoji: '🧥', tone: '#5c9a5b', shape: 'jacket' },
  { id: 'yellow-pants', name: 'Yellow Pants', category: 'Bottoms', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#f0c93a', shape: 'pants' },
  { id: 'yellow-sandals', name: 'Yellow Sandals', category: 'Shoes', colour: 'Yellow', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#f0c93a', shape: 'sandal' },
  { id: 'green-heels', name: 'Green Heels', category: 'Shoes', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#5c9a5b', shape: 'heel' },
  { id: 'orange-hoodie', name: 'Orange Hoodie', category: 'Tops', colour: 'Orange', occasion: 'Casual', weather: 'Rainy', emoji: '👕', tone: '#e87a2e', shape: 'hoodie' },
  { id: 'orange-maxi-dress', name: 'Orange Maxi Dress', category: 'Dresses', colour: 'Orange', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#e87a2e', shape: 'longdress' },
  { id: 'pink-shorts', name: 'Pink Shorts', category: 'Bottoms', colour: 'Pink', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#eba3b8', shape: 'shorts' },
  { id: 'orange-coat', name: 'Orange Coat', category: 'Outerwear', colour: 'Orange', occasion: 'Formal', weather: 'Rainy', emoji: '🧥', tone: '#e87a2e', shape: 'coat' },
  { id: 'purple-sandals', name: 'Purple Sandals', category: 'Shoes', colour: 'Purple', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#7d55a8', shape: 'sandal' },
  { id: 'orange-wide-leg-pants', name: 'Orange Wide-Leg Pants', category: 'Bottoms', colour: 'Orange', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#e87a2e', shape: 'widepants' },
  { id: 'brown-coat', name: 'Brown Coat', category: 'Outerwear', colour: 'Brown', occasion: 'Formal', weather: 'Cloudy', emoji: '🧥', tone: '#6b4a36', shape: 'coat' },
  { id: 'purple-pants', name: 'Purple Pants', category: 'Bottoms', colour: 'Purple', occasion: 'Formal', weather: 'Cloudy', emoji: '👖', tone: '#7d55a8', shape: 'pants' },
  { id: 'beige-dress', name: 'Beige Dress', category: 'Dresses', colour: 'Beige', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#c9a774', shape: 'dress' },
  { id: 'white-wide-leg-pants', name: 'White Wide-Leg Pants', category: 'Bottoms', colour: 'White', occasion: 'Party', weather: 'Cloudy', emoji: '👖', tone: '#e6e5df', shape: 'widepants' },
  { id: 'blue-sandals', name: 'Blue Sandals', category: 'Shoes', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '👡', tone: '#4a72b0', shape: 'sandal' },
  { id: 'green-boots', name: 'Green Boots', category: 'Shoes', colour: 'Green', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#5c9a5b', shape: 'boot' },
  { id: 'grey-boots', name: 'Grey Boots', category: 'Shoes', colour: 'Grey', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#8e8f92', shape: 'boot' },
  { id: 'green-maxi-dress', name: 'Green Maxi Dress', category: 'Dresses', colour: 'Green', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#5c9a5b', shape: 'longdress' },
  { id: 'beige-maxi-dress', name: 'Beige Maxi Dress', category: 'Dresses', colour: 'Beige', occasion: 'Formal', weather: 'Sunny', emoji: '👗', tone: '#c9a774', shape: 'longdress' },
  { id: 'black-pants', name: 'Black Pants', category: 'Bottoms', colour: 'Black', occasion: 'Casual', weather: 'Sunny', emoji: '👖', tone: '#2b2a2f', shape: 'pants' },
  { id: 'grey-heels', name: 'Grey Heels', category: 'Shoes', colour: 'Grey', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#8e8f92', shape: 'heel' },
  { id: 'orange-heels', name: 'Orange Heels', category: 'Shoes', colour: 'Orange', occasion: 'Formal', weather: 'Sunny', emoji: '👠', tone: '#e87a2e', shape: 'heel' },
  { id: 'orange-sneakers', name: 'Orange Sneakers', category: 'Shoes', colour: 'Orange', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#e87a2e', shape: 'shoe' },
  { id: 'pink-sneakers', name: 'Pink Sneakers', category: 'Shoes', colour: 'Pink', occasion: 'Casual', weather: 'Rainy', emoji: '👟', tone: '#eba3b8', shape: 'shoe' },
  { id: 'red-mini-skirt', name: 'Red Mini Skirt', category: 'Bottoms', colour: 'Red', occasion: 'Casual', weather: 'Sunny', emoji: '👗', tone: '#c0392f', shape: 'miniskirt' },
  { id: 'white-sneakers', name: 'White Sneakers', category: 'Shoes', colour: 'White', occasion: 'Casual', weather: 'Sunny', emoji: '👟', tone: '#e6e5df', shape: 'shoe' },
  { id: 'red-boots', name: 'Red Boots', category: 'Shoes', colour: 'Red', occasion: 'Casual', weather: 'Rainy', emoji: '🥾', tone: '#c0392f', shape: 'boot' },
  { id: 'brown-heels', name: 'Brown Heels', category: 'Shoes', colour: 'Brown', occasion: 'Party', weather: 'Sunny', emoji: '👠', tone: '#6b4a36', shape: 'heel' },
  { id: 'grey-sneakers', name: 'Grey Sneakers', category: 'Shoes', colour: 'Grey', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#8e8f92', shape: 'shoe' },
  { id: 'orange-boots', name: 'Orange Boots', category: 'Shoes', colour: 'Orange', occasion: 'Party', weather: 'Cloudy', emoji: '🥾', tone: '#e87a2e', shape: 'boot' },
  { id: 'white-mini-skirt', name: 'White Mini Skirt', category: 'Bottoms', colour: 'White', occasion: 'Party', weather: 'Sunny', emoji: '👗', tone: '#e6e5df', shape: 'miniskirt' },
  { id: 'blue-tee', name: 'Blue Tee', category: 'Tops', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👕', tone: '#4a72b0', shape: 'top' },
  { id: 'blue-shorts', name: 'Blue Shorts', category: 'Bottoms', colour: 'Blue', occasion: 'Casual', weather: 'Sunny', emoji: '🩳', tone: '#4a72b0', shape: 'shorts' },
  { id: 'black-dress', name: 'Black Dress', category: 'Dresses', colour: 'Black', occasion: 'Formal', weather: 'Cloudy', emoji: '👗', tone: '#2b2a2f', shape: 'dress' },
  { id: 'blue-sneakers', name: 'Blue Sneakers', category: 'Shoes', colour: 'Blue', occasion: 'Casual', weather: 'Cloudy', emoji: '👟', tone: '#4a72b0', shape: 'shoe' }
]
const targets = ['silk-blouse', 'brown-pants', 'white-sneakers'].map(id => wardrobe.find(item => item.id === id))
// Look the same as a target but have a different occasion or weather tag, so they do not count
const decoyIds = ['green-blouse', 'brown-trousers', 'white-trainers']
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
const tagGroups = { Occasion: ['Formal', 'Casual', 'Party'], Weather: ['Sunny', 'Rainy', 'Cloudy'], Colours: ['Green', 'Brown', 'White', 'Black', 'Grey', 'Beige', 'Blue', 'Pink', 'Red', 'Yellow', 'Purple', 'Orange'] }
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
    wrong_picks: collected.value.filter(id => !targets.some(t => t.id === id)).length,
    decoy_picks: collected.value.filter(id => decoyIds.includes(id)).length,
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
        <!-- Stays at the top while scrolling so search, tabs and the filter button are always reachable -->
        <div class="sticky-controls">
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


        <div v-if="version === 'A'" class="tabs"><button v-for="cat in categories" :key="cat" :class="{ active: category === cat }" @click="setCategory(cat)">{{ cat }}</button></div>
        <template v-else>
          <div class="search-wrap"><AppIcon name="search" /><input v-model="query" aria-label="Search your wardrobe" type="search" placeholder="Search clothing, colour or tag..." autocomplete="off" /></div>
        </template>
        </div>

        <div class="item-grid" :class="{ 'two-col': inCategory }">
          <button v-for="item in visible" :key="item.id" class="item-card" @click="openItem(item)">
            <ClothingImage :item="item" />
            <div class="item-title">{{ item.name }}</div>
            <div class="item-meta">{{ inCategory ? item.colour : item.category }}</div>
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
